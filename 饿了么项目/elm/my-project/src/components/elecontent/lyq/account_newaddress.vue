<template>
    <div class="account_newaddress">
     <!-- 头部 -->
      <div class="hand">
        <!-- 返回 -->
<span class="el-icon-arrow-left" @click="$router.back(-1)"></span>    
<div class="title_head">  
      <span class="title_text">新增地址</span>
    </div>
    
    </div>
    <div class="profile-1reTe">
            <ul>
            <li>
                <div class="myorder-div">
                <input v-model="name" type="text" placeholder="请填写你的姓名">
                </div>
                </li>
                <li>
                <div class="myorder-div"> <router-link to="/addDetail">
                <!-- <input v-model="this.$route.query.address" type="text" placeholder="小区/写字楼/学校等" > -->
                   <input v-model="address" type="text" placeholder="小区/写字楼/学校等" >
                 </router-link>
                </div>
                </li>
                <li>
                <div class="myorder-div">
                <input v-model="address_detail" type="text" placeholder="请填写详细送餐地址">
                </div>
                </li>
                <li>
                <div class="myorder-div">
                <input v-model="phone" type="text" placeholder="请填写能够联系到您的手机号">
                </div>
                </li>
                <li>
                <div class="myorder-div">
                <input v-model="phone_bk" type="text" placeholder="备用联系电话（选填）">
                </div>
                </li>
            </ul>
            </div>
            <div class="login_container" @click="newadd()">新增地址</div>
    </div>
</template>

<script>
import account_editoraddress from "../lyq/account_editoraddress";
export default {
  name: "account_newaddress",
  data() {
    return {
      user_id: "",
      address: this.$route.query.address,
      address_detail: "",
      // geohash: "3454",
      name: "",
      phone: "",
      // tag: "43",
      // sex: "1",
      phone_bk: ""
      // tag_type: "2"
    };
  },
  components: {
    account_editoraddress
  },
  methods: {
    newadd() {
      let api28 =
        "https://elm.cangdu.org/v1/users/" +
        this.$store.state.usermsg.user_id +
        "/addresses/";
      this.$http({
        method: "post",
        url: api28,
        data: {
          user_id: this.user_id,
          address: this.address,
          address_detail: "454",
          geohash: "354",
          name: this.name,
          phone: this.phone,
          tag: "efrd",
          sex: "1",
          phone_bk: this.phone_bk,
          tag_type: "215654"
        },
        withCredentials: true
      }).then(res => {
        console.log(res);
        var address_detail = this.address_detail;
        var address = this.address;
        var name = this.name;
        var phone = this.phone;
        var phone_bk = this.phone_bk;
        if (
          address_detail == "" ||
          address_detail == undefined ||
          address_detail == null ||
          address == "" ||
          address == undefined ||
          address == null ||
          name == "" ||
          name == undefined ||
          name == null ||
          phone == "" ||
          phone == undefined ||
          phone == null
        ) {
          alert("输入值不能为空");
          return;
        } else {
          var s = /^([\u4e00-\u9fa5|\w]){2,7}$/; //名字和地址
          var r = /^1[3|5|7|8|9][0-9]{9}$/; //手机号判断
          var q = s.test(address_detail);
          var w = s.test(address);
          var e = s.test(name);
          var t = r.test(phone);
          var y = r.test(phone_bk);
          if (q == false||w ==false||e==false||t==false) {
            alert("格式有误,请重新输入");
            return;
          } else {
            if (res.data.status) {
              alert(res.data.success);
              this.$router.push({ name: "account_editoraddress" });
            } else {
              alert(res.data.message);
            }
          }
        }
      });
    }
  }
};
</script>

<style scoped>
* {
  padding: 0;
  margin: 0;
}
/*头部 */
p,
span {
  font-family: Helvetica Neue, Tahoma, Arial;
}
.hand {
  text-align: center;
  background-color: #3190e8;
  border-bottom: 0.01rem ridge rgb(201, 187, 187);
}
.el-icon-arrow-left {
  float: left;
  line-height: 3rem;
  text-decoration-line: none;
  font-weight: bold;
  color: #fff;
  font-size: 1.2rem;
  margin-left: 0.4rem;
}
.title_head {
  width: 50%;
  height: 2.8rem;
  margin: 0 auto;
  line-height: 3rem;
}
.title_text {
  font-size: 1.1rem;
  color: rgb(255, 255, 255);
  font-weight: bold;
}
.profile-1reTe {
  background-color: #fff;
  /* width: 100%; */
  margin: 0.6rem 0;
}
.profile-1reTe ul li {
  height: 3rem;
  /* width: 100%; */
  text-align: center;
}
.myorder-div {
  /* width: 9rem; */
  width: 90%;
  height: 3rem;
  float: left;
  text-align: center;
}

/*表单*/
ul li {
  height: 3.1rem;
  /* width: 100%; */
  line-height: 3.1rem;
}
.myorder-div input {
  display: block;
  /* width: 22rem; */
  width: 100%;
  font-size: 0.9rem;
  margin: 0.4rem 4%;
  padding: 0.5rem 0.3rem;
  background: #f0efef;
  border: 1px solid #ddd;
  /* border-radius: 0.4rem; */
  /* margin: 0 auto; */
}
/* 确认button*/
.login_container {
  margin: 0 0.5rem 1rem;
  font-size: 1.1rem;
  color: #fff;
  background-color: #4cd964;
  padding: 0.7rem 0;
  border: 1px;
  border-radius: 0.15rem;
  text-align: center;
}
</style>

