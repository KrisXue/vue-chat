<template>
    <div class="modal-dialog" v-bind:class="{'show': show}" >
        <div class="modal-content">
            <!-- <div class="modal-header">
                昵称
            </div> -->
            <div class="modal-body">
                <!-- <el-input v-model="userId" placeholder="UserId"></el-input><br><br> -->
                <el-input v-model="userName" placeholder="昵称"></el-input>
            </div>
            <div class="modal-footer" >
                <button class="btn btn-primary" v-on:click="loginPro" >进入</button>
            </div>
        </div>
    </div>
</template>

<script>
import { getBusCxt } from '../store'
export default {
  name: 'Login',
  data () {
    return {
      userId: null,
      userName: null,
      show: true
    }
  },
  created () {
    this.userName = window.sessionStorage.getItem('userName') || ''
    if (this.userName !== '') {
      this.show = false
    }
  },
  methods: {
    loginPro () {
      if (this.userName) {
        this.show = false
        getBusCxt().userCxt.registerUser(this.guid(), this.userName)
        window.sessionStorage.setItem('userName', this.userName)
      }
    },
    guid () {
      return 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function (c) {
        // eslint-disable-next-line one-var
        const r = Math.random() * 16 | 0,
          v = c === 'x' ? r : (r & 0x3 | 0x8)
        return v.toString(16)
      })
    }
  }
}
</script>>

<style>
  .modal-dialog.show {
    position: absolute;
    top: 50%;
    left: 50%;
    margin-top: -120px;
    margin-left: -300px;
    opacity: 1;
  }
  .modal-dialog {
    opacity: 0;
    display: none;
  }
</style>
