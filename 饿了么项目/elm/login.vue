<template>
  <div>
    <div>
      <input v-model="username" type="text" placeholder="用户名">

    </div>

    <div>
      <input v-model="password" type="text" placeholder="密码">

    </div>
    <div>
      <input v-model="codeNumer" type="text" placeholder="验证码">
      <img @click="getCode()" :src="code&&code" alt="">

    </div>

    <hr>
    <button @click="login()">login</button>
    <button @click="login2()">login</button>

  </div>

</template>


<script>
  export default {
    name: "login",
    data() {
      return {
        code: "",
        username: "",
        password: "",
        codeNumer: ""
      }
    },
    created() {
      this.getCode();

    },
    methods: {
      getCode() {
        const url = "https://elm.cangdu.org/v1/captchas";
        // ----------------------------------
        this.$http({
          method: 'post',
          url: url,
//https://developer.mozilla.org/zh-CN/docs/Web/API/Request/credentials
        //用于表示用户代理是否应该在跨域请求的情况下从其他域发送cookies。
          withCredentials: true, // 默认false
        }).then((res) => {
          console.log('tap', res);
            if(res.data.status == 200){}
          this.code = res.data.code
        });
      },
      login() {
        const api = "https://elm.cangdu.org/v2/login";
        this.$http({
          method: 'post',
          url: api,
          withCredentials: true, // 默认的
            data: {
              captcha_code: this.codeNumer,
              password: "syq1122",
              username: "syq1122"
            },

        }).then(res => {
          alert("登陆成功");  
          console.log('---', res)
          //给vuex保存用户信息
this.$router.push({name:"person",query:res.data});
        });

      }
    }
  }

</script>
<style>
</style>
