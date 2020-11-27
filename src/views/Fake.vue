<template>
  <div style="background-color: #f7f3f3">
    <mt-header title="请假报备" style="background-color: #04C8E3;font-size: 18px"></mt-header>
    <mt-navbar v-model="selected">
      <mt-tab-item id="1" style="padding-top: 10px">请假报备</mt-tab-item>
      <mt-tab-item id="2" style="padding-top: 10px">报备记录</mt-tab-item>
    </mt-navbar>

    <mt-tab-container v-model="selected">
      <mt-tab-container-item id="1">
        <mt-field label="请假人" readonly placeholder="姓名" v-model="username" ></mt-field>
        <mt-field label="辅导员" readonly placeholder="杨建波" v-model="teacher" style="margin-top: 5px"></mt-field>
        <mt-cell
          style="margin-top: 5px"
          class="black"
          title="请假类型"
          is-link
          value="事假">
        </mt-cell>
        <mt-cell
          style="margin-top: 5px"
          title="开始时间"
          is-link
          >
          <mt-button class="text-button" v-on:click="start">请选择</mt-button>
        </mt-cell>
        <mt-cell
          title="结束时间"
          to="#"
          is-link>
          <mt-button class="text-button" v-on:click="end">请选择</mt-button>
        </mt-cell>
        <mt-cell
          title="请假时长"
          >
          <mt-button class="text-button" v-on:click="duration">0天</mt-button>
        </mt-cell>
        <img :src='`${publicPath}shuoming.PNG`' class="shuoming"  >
        <div v-on:click="why">
        <mt-field label="请假事由" type="textarea" rows="4" style="text-align: left" placeholder="(40字以内)" >

        </mt-field>
        </div>
        <mt-field label="离校去向" >
          <mt-button class="text-button" v-on:click="whereugoing">请输入离校去向</mt-button>
        </mt-field>
        <mt-field label="紧急联系人" >
          <mt-button class="text-button" v-on:click="who">请输入紧急联系人</mt-button>
        </mt-field>
        <mt-field label="紧急联系人电话" >
          <mt-button class="text-button" v-on:click="who_tel">请输入紧急联系人电话</mt-button>
        </mt-field>
        <mt-button type="primary" style="width: 40%;margin: 10px auto">提交</mt-button>
      </mt-tab-container-item>
      <mt-tab-container-item id="2">
        <div class="fake-vacation">
          <div class="status-bar">
            <div class="name">{{username}}</div>
            <div class="pass">已通过</div>
          </div>
          <div class="vacation-info" v-on:click="look">
            <div class="va-type">请假类型: {{vatype}}</div>
            <div class="va-type">开始时间: {{sTime}}</div>
            <div class="va-type">结束时间: {{eTime}}</div>
            <div class="va-type">请假时长: {{durationTime}}</div>
          </div>
        </div>
        <div>
          <p>没有检索到更多数据！</p>
        </div>
        <mt-popup
          v-model="popupVisible"
          position="bottom">
          <div class="tips" >
            <img :src='`${publicPath}logo.PNG`' class="logo">
            <img :src='`${publicPath}wrong.png`' v-on:click="look" class="wrong">
            <table class="info-table" >
              <tr >
                <td class="info-table-title" align="right">类型:</td>
                <td><span class="gray">{{vatype}}</span></td>
              </tr>
              <tr>
                <td align="right">请假人:</td>
                <td><span class="gray">{{username}}</span></td>
              </tr>
              <tr>
                <td align="right">辅导员:</td>
                <td><span class="gray">{{teacher}}</span></td>
              </tr>
              <tr>
                <td align="right">申请时间:</td>
                <td><span class="gray">{{applyTime}}</span></td>
              </tr>
              <tr>
                <td align="right">开始时间:</td>
                <td><span class="gray">{{sTime}}</span></td>
              </tr>
              <tr>
                <td align="right">结束时间:</td>
                <td><span class="gray">{{eTime}}</span></td>
              </tr>
              <tr>
                <td align="right">请假时长:</td>
                <td><span class="gray">{{durationTime}}</span></td>
              </tr>
              <tr>
                <td align="right">请假事由:</td>
                <td><span class="gray">{{introduction}}</span></td>
              </tr>
              <tr>
                <td align="right">离校去向:</td>
                <td><span class="gray">{{whereugo}}</span></td>
              </tr>
            </table>
              <table style="padding-left: 5%">
              <tr>
                <td align="left" s>紧急联系人:</td>
                <td><span class="gray">{{contact}}</span></td>
              </tr>
              </table>
            <table  style="padding-left: 5%">
              <tr>
                <td align="left">紧急联系人电话:</td>
                <td><span class="gray">{{contact_tel}}</span></td>
              </tr>
<!--              <tr>-->
<!--                <td colspan="2">-->
<!--                  <img :src='img_url' class="up_img" v-on:click="viewPhoto">-->
<!--                </td>-->
<!--              </tr>-->
            </table>

          </div>
        </mt-popup>
<!--        <mt-popup-->
<!--          v-model="photoVisible"-->
<!--          >-->
<!--          <img :src='img_url' class="up_img_big">-->
<!--        </mt-popup>-->
      </mt-tab-container-item>
    </mt-tab-container>
  </div>
</template>
<script>
export default {
  name: 'Fake',
  data: function () {
    return {
      photoVisible: false,
      publicPath: process.env.BASE_URL,
      popupVisible: false,
      selected: 1,
      // 申请时间
      applyTime: '',
      // 用户名
      username: '姓名',
      // 辅导员
      teacher: '杨建波',
      // 请假类型
      vatype: '事假',
      // 开始时间
      sTime: '',
      // 开始小时,用来计算
      sHour: '',
      // 结束时间
      eTime: '',
      // 结束小时，用来计算
      eHour: '',
      // 请假时长
      durationTime: '',
      // 请假事由
      introduction: '家中有事',
      // 离校去向
      whereugo: '郑州市金水区',
      // 紧急联系人: '',
      contact: '杨英建',
      // 紧急联系人电话
      contact_tel: '15903654609',
      // 图片路径
      img_url: 'https://images1.pianshen.com/101/9d/9d01938f2724cbe251a61f7016d5eb95.png'
    }
  },
  created: function () {
    // `this` 指向 vm 实例
    var date = new Date()
    const year = date.getFullYear()
    const month = date.getMonth() + 1
    const day = date.getDate()
    const startHour = '08:00'
    const endHour = '20:00'
    const duration = '0天12时'
    this.applyTime = year + '-' + month + '-' + (day - 1) + ' ' + '09:00'
    this.sTime = year + '-' + month + '-' + day + ' ' + startHour
    this.sHour = '8'
    this.eHour = '20'
    this.eTime = year + '-' + month + '-' + day + ' ' + endHour
    this.durationTime = duration
    console.log(this.applyTime)
    console.log(this.sTime)
    console.log(this.eTime)
    this.duration()
  },
  methods: {
    viewPhoto () {
      this.photoVisible = !this.photoVisible
    },
    // 开始时间
    start () {
      this.$messagebox.prompt('请输入开始小时(如:08，系统会自动补上今天的年月日)').then(({ value, action }) => {
        if (action === 'confirm') {
          const date = new Date()
          const year = date.getFullYear()
          const month = date.getMonth() + 1
          const day = date.getDate()
          this.sHour = value
          this.sTime = year + '-' + month + '-' + day + ' ' + this.sHour + ':00'
          this.duration()
        }
      })
    },
    // 返校时间
    end () {
      this.$messagebox.prompt('请输入返校时间-单位小时(例20),系统会自动补全并计算请假时间').then(({ value, action }) => {
        if (action === 'confirm') {
          const date = new Date()
          const year = date.getFullYear()
          const month = date.getMonth() + 1
          const day = date.getDate()
          this.eHour = value
          this.eTime = year + '-' + month + '-' + day + ' ' + this.eHour + ':00'
          this.duration()
        }
      })
    },
    // 时间段设置
    duration () {
      this.durationTime = '0天' + (this.eHour - this.sHour) + '时'
    },
    // 请假事由事件
    why () {
      this.$messagebox.prompt('请输入请假事由').then(({ value, action }) => {
        if (action === 'confirm') {
          this.introduction = value
        }
      })
    },
    // 离校去向
    whereugoing () {
      this.$messagebox.prompt('请输入离校去向').then(({ value, action }) => {
        if (action === 'confirm') {
          this.whereugo = value
        }
      })
    },
    // 紧急联系人
    who () {
      this.$messagebox.prompt('请输入紧急联系人').then(({ value, action }) => {
        if (action === 'confirm') {
          this.contact = value
        }
      })
    },
    // 紧急联系人电话
    who_tel () {
      this.$messagebox.prompt('请输入紧急联系人电话').then(({ value, action }) => {
        if (action === 'confirm') {
          this.contact_tel = value
        }
      })
    },
    // 申请日期
    set_apply_time () {
      this.$messagebox.prompt('请输入申请日期(例:2020-11-14 08:00)').then(({ value, action }) => {
        if (action === 'confirm') {
          this.applyTime = value
        }
      })
    },
    // 详细信息
    look () {
      this.popupVisible = !this.popupVisible
    }
  }
}
</script>

<style>
.up_img_big {
  width: 80%;
  height: 50%;
}
.up_img {
  margin-top: 10px;
  width: 60px;
  height: 40px;
  /*border: 1px solid;*/
}
textarea{
  text-align: left!important;
}
body {
  background-color: #f7f3f3;
}
.height {
  height: 30px;
}
.mint-tab-item{
  height: 10px !important;
}
.mint-tab-item-label {
  font-size: 16px !important;
}
.mint-navbar {
  height: 37px;
}
.mint-tab-container {
  margin-top: 10px;
}
.mint-field-core{
  text-align: right !important;
  padding-right: 40% !important;
}
.mint-cell-value {
  color: black !important;
}
.mint-popup{
  width: 100%;
}
.mint-cell-title{
  text-align: left;
  /*padding-left: 5%;*/
}
.mint-cell-title{
  width: 40% !important;
}
.mint-field-core{
  text-align: left ;
}
.black {
  color: black !important;
}

.fake-vacation {
  padding-left: 2%;
  padding-right: 2%;
  background-color: white;
  width: 96%;
  height: 140px;
  /*border: 1px solid black;*/
}
.status-bar{
  width: 100%;
  height: 20px;
  /*border: 1px solid;*/
}
.pass {
  margin-top: 7px;
  font-size: 15px;
  float: right;
  display: inline;
  color: #05C729;
  text-align: right;
}
.name {
  margin-top: 7px;
  font-size: 15px;
  display: inline;
  float: left;
  text-align: left;
}
.mint-tab-container {
  /*height: 800px;*/
}
.vacation-info{
  margin-top: 10px;
  color: #A0A8A9;
  line-height: 27px;
  text-align: left;
  font-size: 15px;
  /*border: 1px solid;*/
}
.text-button {
  background-color: white !important;
  color: #A0A8A9 !important;
  border: 0 !important;
  box-shadow: none !important;
  font-size: 16px !important;
}
.mint-button {
  padding-right: 0px !important;
}
.tips {
  border-radius: 50px;
  text-align: left;
  width: 90%;
}
.mint-popup-bottom {
  padding-bottom: 5%;
  top: -29% !important;
  width: 86% !important;
  height: 78% !important;
}
.mint-popup{
  border-radius: 4px;
  position: relative;
}
.gray {
  padding-left: 10px;
  color: gray;
}
.info-table {
  line-height: 30px;
  margin-left: 5%;
  margin-top: 2%;
}
.info-table-title {
  width: 35%;
}
.logo {
  width: 25%;
  margin-top: 3%;
}
.wrong {
  position: absolute;
  right: -4%;
  top: -1.6%;
  width: 6%;
  border: 3px solid white;
  border-radius: 50%;
}
.mint-cell-title {
  width: 33% !important;
}
.why-button {
  color: gray;
  border: 1px solid;
  width: 100%;
  height: 100px;
}
.shuoming {

  margin-top: 2%;
  width: 100%;
}
</style>
