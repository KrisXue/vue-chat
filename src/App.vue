<template>
  <div id="app">  
    <div class="head">
      <!-- <span v-if="getRoomInfo != null" >当前房间名称：{{getRoomInfo.name}}</span> -->
      <!-- <button class="btn btn-primary" v-on:click="loginOut" >登出</button> -->
      <!-- <span v-if="userName !== ''" >当前用户：{{userName}}</span> -->
    </div>
    <div class="cont">
      <HChat></HChat>
      <Login></Login>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import { Keys } from './uitls'
import HChat from './components/HChat'
import Login from './components/Login'
import { getBusCxt } from './store'

let currRoom = Keys.GETROOMINFO

export default {
  name: 'app',
  data () {
    return {
      userName: ''
    }
  },
  created () {
    this.userName = window.sessionStorage.getItem('userName')
  },
  components: {
    HChat,
    Login
  },
  computed: {
    ...mapGetters([currRoom])
  },
  methods: {
    loginOut: function () {
      getBusCxt().userCxt.closeConn()
    }
  }
}
</script>

<style lang="scss" >
  $head-height: 30px;

html, body, #app, .cont{
  height: 100%;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.head{
  height: $head-height;  
  line-height:$head-height;
  padding: 10px;
  text-align: right;
  background: -webkit-linear-gradient( left top,#20A0FF,#58B7FF);
}
.cont{
  margin-top: -$head-height;
  padding-top: $head-height;
}
</style>
