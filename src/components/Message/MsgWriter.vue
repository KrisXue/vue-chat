<template>
    <div style="height: 100%; position: relative;" >
        <el-input type="textarea" :rows="7" v-model="cont" @keyup.enter.native="add"></el-input>
        <div class="btn-group btn-group-custom" >
          <button type="button" class="btn btn-primary" @click="add" >发送</button>          
        </div>
    </div>
</template>
<script>
import { getBusCxt } from '../../store'
export default {
  name: 'MsgWriter',
  data () {
    return {
      cont: ''
    }
  },
  methods: {
    add: function () {
      if (this.cont === '' || this.cont.replace(/\s/g, '') === '') {
        return false
      }
      /* 组件 */
      let msg = {cont: this.cont, time: this.timeFormate(new Date())}
      getBusCxt().msgCxt.sendMsg(msg)
      this.cont = ''
      this.$parent.fatherMethod()
    },
    timeFormate: function (timeStamp) {
      let year = new Date(timeStamp).getFullYear()
      let month =
        new Date(timeStamp).getMonth() + 1 < 10
          ? '0' + (new Date(timeStamp).getMonth() + 1)
          : new Date(timeStamp).getMonth() + 1
      let date =
        new Date(timeStamp).getDate() < 10
          ? '0' + new Date(timeStamp).getDate()
          : new Date(timeStamp).getDate()
      let hh =
        new Date(timeStamp).getHours() < 10
          ? '0' + new Date(timeStamp).getHours()
          : new Date(timeStamp).getHours()
      let mm =
        new Date(timeStamp).getMinutes() < 10
          ? '0' + new Date(timeStamp).getMinutes()
          : new Date(timeStamp).getMinutes()
      let ss =
        new Date(timeStamp).getSeconds() < 10
          ? '0' + new Date(timeStamp).getSeconds()
          : new Date(timeStamp).getSeconds()
      return year + '-' + month + '-' + date + ' ' + hh + ':' + mm + ':' + ss
    }
  }
}

</script>
<style lang="scss" scoped >
  .btn-group-custom{
    position: absolute;
    width: 100%;
    bottom: 0;
    left: 0;
    padding: 10px;
  }
  .btn-group-custom .btn {
    float: right;
  }
</style>