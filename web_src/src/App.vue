<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'app',
  data(){
    return {
      isLogin: false,
      userInfo: { //保存用户信息
        nick: null,
        ulevel: null,
        uid: null,
        portrait: null
      }
    }
  },
  created() {
    if(!this.$cookies.get("session")){
      //如果没有登录状态则跳转到登录页
      this.$router.push('/login');
    }
  },
  //监听路由检查登录
  watch:{
    "$route" : 'checkLogin'
  },
  mounted(){
    //组件开始挂载时获取用户信息
    // this.getUserInfo();
  },
  methods: {
    //请求用户的一些信息
    getUserInfo(){
      var userinfo = this.$cookies.get("session");
    },
    checkLogin(){
      //检查是否存在session
      //cookie操作方法在源码里有或者参考网上的即可
      if(!this.$cookies.get("session")){
        //如果没有登录状态则跳转到登录页
        this.$router.push('/login');
      }
    },
    getCookie: function (cname) {
      var name = cname + "=";
      var ca = document.cookie.split(';');
      for (var i = 0; i < ca.length; i++) {
        var c = ca[i];
        while (c.charAt(0) == ' ') c = c.substring(1);
        if (c.indexOf(name) != -1) return c.substring(name.length, c.length);
      }
      return "";
    }
  },
  components: {}
};
</script>

<style>
html,
body,
#app {
  margin: 0 0;
  background-color: #e9eef3;
  height: 100%;
}
.el-header,
.el-footer {
  /* background-color: #b3c0d1; */
  color: #333;
  text-align: center;
  line-height: 60px;
}
.el-main {
  background-color: #e9eef3;
  color: #333;
  text-align: center;
  padding-top: 0px !important;
}

/*定义滚动条高宽及背景 高宽分别对应横竖滚动条的尺寸*/
::-webkit-scrollbar {
  width: 8px;
  height: 8px;
}

/*定义滚动条轨道 内阴影+圆角*/
::-webkit-scrollbar-track {
  border-radius: 4px;
  background-color: #F5F5F5;
}

/*定义滑块 内阴影+圆角*/
::-webkit-scrollbar-thumb {
  border-radius: 4px;
  background-color: #c8c8c8;
  box-shadow: inset 0 0 6px rgba(0, 0, 0, .1);
  -webkit-box-shadow: inset 0 0 6px rgba(0, 0, 0, .1);
}
</style>
