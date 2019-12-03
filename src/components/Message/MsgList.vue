<template> 
    <div>
        <ul class="msg-cont">
            <li v-for="(item,index) in getNewMsg"  :key="index" :class="item.type === 'send' ?'msg-cont-send': 'msg-cont-receive'" >
                <p>{{item.time}}</p>
                <span>{{item.type === 'send' ? '我':item.userName}}: </span><span class="msg-cont-item" >{{item.cont}}</span>
            </li>
        </ul>
    </div>
</template>
<script>
  import { mapGetters } from 'vuex'
  import { Keys } from '../../uitls'
  let recKey = Keys.GETNEWMSG
  export default{
    name: 'MsgList',
    computed: {
      ...mapGetters([recKey])
    },
    watch: {
      getNewMsg: function (val) {
        console.log(val)
        this.$parent.fatherMethod()
      }
    }
  }
</script>
<style lang="scss" scoped >
    .msg-cont{
        list-style-type: none;
        margin: 0px;
        padding: 0px;
    }
    .msg-cont > li{
        margin: 0px;
        padding: 5px;
    }
    .msg-cont-receive .msg-cont-item{
        padding: 5px 10px; 
        border-radius: 2px;
        margin-bottom: 5px;
        background:#F5F5F5;
    }
    .msg-cont-receive {
        text-align: left;
    }
    .msg-cont-send .msg-cont-item{
        padding: 5px 10px; 
        border-radius: 2px;
        margin-bottom: 5px;
        background: #ADD8E6;
    }
    .msg-cont-send{
        text-align: right;
    }
</style>