<template>
    <div class="saetch">
     <!-- 头部 -->
      <div class="hand">
        <!-- 返回 -->
  <router-link class="el-icon-arrow-left" to="/Aaa"></router-link>
    <div class="title_head">  
      <span class="title_text">搜索</span>
    </div> 
    </div>
    <form class="content">
      <input type="search" placeholder="请输入商家或美食名称" v-model="name">
      <input type="submit" value="提交" @click="submit()">
    </form>
    <div class="bottom" v-show="show">很抱歉！无搜索结果</div>
    <wode></wode>
    </div>
</template>

<script>
import wode from "../elecontent/wode";
export default {
  name: "saetch",
  components: {
    wode
  },
  data() {
    return {
      data: [],
      show: false,
      name: ""
    };
  },
  watch: {
    name(newvalue) {
      if (newvalue == 0) {
        this.show = false;
      }
    }
  },
  methods: {
    submit() {
      this.show = true;
    }
  },
  created() {
    var botchoice = {
      waimai: false,
      sousuo: true,
      dingdan: false,
      mine: false
    };
    this.$store.commit("changebotchoice", botchoice);
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
.saetch {
  background-color: rgb(236, 236, 236);
  width: 100%;
}
.hand {
  text-align: center;
  background-color: #3190e8;
}

.hand {
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
  /* border: 1px solid red; */
}
.title_text {
  font-size: 1.1rem;
  color: rgb(255, 255, 255);
  font-weight: bold;
}
.content {
  background: #fff;
  display: flex;
  width: 100%;
  padding: 1rem;
  /* border: 1px solid red; */
  box-sizing: border-box;
}
.content input:nth-child(1) {
  flex: 4;
  border: 0.2rem solid #e4e4e4;
  font-size: 0.65rem;
  color: #333;
  border-radius: 0.2rem;
  background-color: #f2f2f2;
  font-weight: 700;
  padding: 0 0.3rem;
  /* border: 1px solid red; */
  height: 2rem;
}
.content input:nth-child(2) {
  flex: 1;
  border: 0.2rem solid #3190e8;
  margin-left: 0.2rem;
  font-size: 0.65rem;
  color: #fff;
  border-radius: 0.2rem;
  background-color: #3190e8;
  font-weight: 700;
  padding: 0 0.2rem;
}
.bottom {
  margin: 0 auto;
  font: 0.65rem/1.75rem Microsoft YaHei;
  color: #333;
  background-color: #fff;
  text-align: center;
  margin-top: 0.125rem;
}
</style>

