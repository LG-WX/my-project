<template>
<!--  商品列表-->
    <div class="list">
        <!-- <titleaaa></titleaaa> -->
         <p class="fujin">附近商家</p>
       <div class="merchant-list">
        <p v-for="mls in data6" :key="mls.id" class="merchant-list-single">
         
          <router-link :to="{name:'store',params:{id:mls.id}}">
              <div class="flex">
                <img :src="'https://elm.cangdu.org/img/'+mls.image_path" alt="" class="flex-left">
                <div class="flex-right">
              <div class="flex-right-top mutual">
                <div class="flex-right-top-left"><span class="pinpai">品牌</span>
                <strong class="shoppingname">{{mls.name}}</strong>
                </div>
                <div class="flex-right-top-right">保准票</div>
              </div>
              <div class="flex-right-content mutual">
                <div class="flex-right-content-left">
                  <div class="block">
                       <span class="star">
                         <el-rate v-model="mls.rating" disabled show-score text-color="#ff9900" score-template="{value}">
                         </el-rate>
                   </span> 
                       <span class="yueshou">月售{{mls.recent_order_num}}单</span>
                   </div>
                </div>
                <div class="flex-right-content-right">
                 <b class="fengniao">蜂鸟专送</b> 
                 <b class="zhunshi">准时达</b>
                  </div>
              </div>
              <div class="flex-right-bottom mutual">
                <div class="flex-right-content-left">
                  ¥{{mls.float_minimum_order_amount}}起送/配送费约¥{{mls.float_delivery_fee}}
                </div>
                <div class="flex-right-tocontentp-right">
                  <span class="gongli">{{mls.distance}}/</span>
                  <span class="time">{{mls.order_lead_time}}</span>
                </div>
              </div>
              </div>
             </div>
            </router-link>
             </p>
             </div>
             </div>
</template>
<script>
// element UI
import { Loading } from "element-ui";
export default {
  name: "merchantlist",
  data: () => ({
    data6: [],
    data6b: [],
    data6c: [],
    value5: 3.7,
    id: "",
    suoyouxinxi: [],
    sbdata: "",
    data: [],
    aaa: [],
    Arr: []
  }),
  // 设置属性,便于监听这个属性是否更新
  props: ["cli", "cli2"],
  watch: {
    cli(news, olds) {
      this.data6 = this.data6b;
      this.id = news.id;
      this.data6 = this.data6.filter(function(val) {
        return val.category == news.el;
      });
    },
    cli2(news2, olds2) {
      var _this = this;
      _this.data6 = _this.data6b;
      var arrId = [];
      var storeMsg = [];
      var newArr;
      // 所有数据
      _this.data6.forEach((value, index) => {
        for (var items of value.supports) {
          news2.forEach(element => {
            if (items.name == element) {
              arrId.push(index);
            }
          });
        }
        newArr = Array.from(new Set(arrId));
        // console.log(newArr);
      });
      newArr.forEach(function(value) {
        storeMsg.push(_this.data6[value]);
      });
      // console.log(storeMsg);
      _this.data6 = storeMsg;
    },
    data6(news) {
      // console.log(news);
    },
    id() {
      var _this = this;
      var api6 = "https://elm.cangdu.org/shopping/restaurants";

      this.$http
        .get(api6, {
          params: {
            latitude: localStorage.latitude,
            longitude: localStorage.longitude,
            limit: 100,
            order_by: _this.id
          }
        })
        .then(function(data) {
          //关闭加载提示
          // loadingInstance1.close();
          // 成功后的回调
          console.log("成功了....");
          //展示所有商店名
          console.log(data);
          _this.data6 = data.data;

          console.log(_this.data6);
          _this.data6b = data.data;
        });
    }
  },

  created() {
    let loadingInstance1 = Loading.service({
      fullscreen: true
    });
    // 接口 6
    var _this = this;
    var api6 = "https://elm.cangdu.org/shopping/restaurants";

    this.$http
      .get(api6, {
        params: {
          latitude: localStorage.latitude,
          longitude: localStorage.longitude,
          limit: 20,
          order_by: _this.id
        }
      })
      .then(function(data) {
        //关闭加载提示
        loadingInstance1.close();
        // 成功后的回调
        // console.log("成功了....");
        //展示所有商店名
        _this.data6 = data.data;
        // console.log(_this.data6);
        _this.data6b = data.data;

        _this.suoyouxinxi = _this.data6b[0].supports[1].name;
        // console.log("所有信息" + _this.suoyouxinxi);
      });
  }
  // created(){
  //   // this.$store.commit("getcgid",mls.id)
  //   // console.log(mls.id)
  // }
};
</script>
<style scoped>
.list {
  background: #fff;
}
.flex {
  display: flex;
  align-items: center;
  border-bottom: 1px solid #f1f1f1;
  padding: 0.4rem;
  text-align: center;
}
.merchant-list {
  width: 100%;
  box-sizing: border-box;
}
.flex-left {
  width: 4rem;
  height: 4.5rem;
  margin-right: 0.3rem;
}
.flex-right {
  flex: auto;
}
.mutual {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.flex-right-top-right {
  color: #999;
  width: 4rem;
  text-align: center;
  line-height: 1.3rem;
  height: 1.3rem;
  font-size: 0.6rem;
}
.pinpai {
  color: #333;
  background-color: #ffd930;
  font-size: 0.5rem;
  border-radius: 0.3rem;
  width: 6rem;
  height: 2rem;
}
.shoppingname {
  color: #333;
  font-size: 0.8rem;
  font-weight: 600;
  width: 4rem;
}
.flex-right-content {
  margin: 0.6rem 0;
  line-height: 1rem;
}
.star {
  float: left;
  /* width: 6rem; */
  /* border:1px solid red; */
  height: 1rem;
}
.yueshou {
  float: left;
  color: #666;
  font-size: 0.5rem;
  margin-left: 0.1rem;
}
.fengniao {
  background-color: #3190e8;
  color: white;
  font-size: 0.5rem;
  width: 2rem;
  /* border: 1px solid black; */
}
.zhunshi {
  border: 0.04rem solid #3190e8;
  color: #3190e8;
  width: 2rem;
  font-size: 0.5rem;
}
.fujin {
  margin: 0.4rem;
  font-size: 1rem;
  color: #999;
}
.flex-right-content-left {
  float: left;
  color: #666;
  font-size: 0.8rem;
}
.flex-right-content-right {
  float: right;
}
.gongli {
  color: #666;
  font-size: 0.6rem;
  /* margin-left: 4rem; */
  /* border: 1px solid red; */
}
.flex-right-tocontentp-right {
  /* border: 1px solid red; */
  display: flex;
  justify-content: flex-end;
}
.time {
  color: #3190e8;
  font-size: 0.6rem;
}

</style>
<style>
/* 星星评分 */
<style>  
.el-rate__item {
    margin-top: 0.1rem;
    margin-left: 0.03rem;
    width: 0.087rem;
    /* border: 1px solid green; */
  }

  .el-rate__icon {
    font-size: .05rem;
    /* border: 1px solid green; */
    margin:0;
  }

  .el-rate__text {
    font-size: 0.1rem;
    /* border: 1px solid green; */
  }

</style>
