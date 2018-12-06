<template>
  <header class="header">
    <!-- 顶部通栏开始 -->
    <div class="top-wrapper">
      <div class="back-wrapper">
        <span class="icon-arrow_lift"></span>
      </div>
      <form class="search-wrapper">
        <span class="search-icon"></span>
        <input class="search-bar" type="serach" placeholder="搜索店内信息">
      </form>
      <div class="more-wrapper">
        <a href class="spelling-bt">拼单</a>
        <div class="more-bt">
          <i class="s-radius"></i>
          <i class="s-radius"></i>
          <i class="s-radius"></i>
        </div>
      </div>
    </div>
    <!-- 顶部通栏结束 -->
    <!-- 主题内容开始 -->
    <div class="content-wrapper">
      <div class="icon" :style="head_bg"></div>
      <div class="name">
        <h3>{{poiInfo.name}}</h3>
      </div>
      <div class="collect">
        <img src="./img/star.png" alt>
        <span>收藏</span>
      </div>
    </div>
    <!-- 主题内容结束 -->
    <!-- 公告内容开始 -->
    <div class="bulletin-wrapper">
      <img class="icon" v-if="poiInfo.discounts2" :src="poiInfo.discounts2[0].icon_url">
      
      <span class="text" v-if="poiInfo.discounts2">{{poiInfo.discounts2[0].info}}</span>
      <div class="detail" v-if="poiInfo.discounts2" @click="showBulletin">
        {{poiInfo.discounts2.length}}个活动
        <span class="icon-keyboard_arrow_right"></span>
      </div>
    </div>
    <!-- 公告内容结束 -->
    <!-- 公告详情开始 -->
    <transition name="bulletin-detail">
      <div class="bulletin-detail" v-show="isShow">
        <div class="detail-wrapper">
          <!-- 相关内容容器 -->
          <div class="main-wrapper" :style="detail_bg">
            <div class="icon" :style="head_bg"></div>
            <h3 class="name">{{poiInfo.name}}</h3>
            <!-- 星级评价 -->
            <div class="score">
              <app-star :score="poiInfo.wm_poi_score"></app-star>
              <span>{{poiInfo.wm_poi_score}}</span>
            </div>

            <p class="tip">
              {{poiInfo.min_price_tip}}
              <i>|</i>
              {{poiInfo.shipping_fee_tip}}
              <i>|</i>
              {{poiInfo.delivery_time_tip}}
            </p>

            <p class="time">配送时间: {{poiInfo.shipping_time}}</p>

            <div class="discounts" v-if="poiInfo.discounts2">
              <p>
                <img :src="poiInfo.discounts2[0].icon_url">
                <span>{{poiInfo.discounts2[0].info}}</span>
              </p>
            </div>
          </div>
        

        <!-- 关闭内容容器 -->
          <div class="close-wrapper">
            <span class="icon-close" @click="closeBulletin"></span>
          </div>
        </div>
      </div>
  </transition>
    <!-- 公告详情结束 -->
    <!-- 背景内容开始 -->
    <div class="bg-wrapper" :style="head_pic_url"></div>
    <!-- 背景内容结束 -->
  </header>
</template>

<script>
import Star from '../star/Star'
export default {
  name: "Header",
  props: {
    poiInfo: {
      type: Object,
      default: {}
    }
  },
  components: {
    "app-star": Star
  },
  data() {
    return {
      isShow: false
    };
  },
  computed: {
    head_pic_url(){
      return "background-image: url(" + this.poiInfo.head_pic_url + ");"
    },
    head_bg(){
      return "background-image: url(" + this.poiInfo.pic_url + ");"
    },
    detail_bg(){
      return "background-image: url(" + this.poiInfo.poi_back_pic_url + ");"
    }
  },
  methods: {
    showBulletin(){
      this.isShow = true
    },
    closeBulletin(){
      this.isShow = false
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url(../../common/style.css);
header {
  height: 130px;
  padding-top: 20px;
}
.top-wrapper{
  /* background: cornflowerblue; */
  position: relative;
}
.top-wrapper .back-wrapper{
  position: absolute;
  left: 0;
  top: 0;
  height: 31px;
  line-height: 31px;
  /* background: aquamarine; */
}
.top-wrapper .back-wrapper span{
  color: white;
  display: inline-block;
  margin-left: 15px;
}
.top-wrapper .search-wrapper {
  box-sizing: border-box;
  padding: 0 104px 0 50px;
  width: 100%;
  height: 31px;

}
.top-wrapper .search-wrapper .search-bar{
  width: 100%;
  height: 31px;
  border-radius: 25px;
  box-sizing: border-box;
  border: 0;
  outline: none;
  background: #cdcdcc;
  padding-left: 28px;
}
.top-wrapper .search-wrapper .search-icon{
  position: absolute;
  left: 50px;
  top: 0px;
  width: 28px;
  height: 31px;
  background: url(./img/search.png) no-repeat 11px center;
  background-size: 13px 13px;

}
.top-wrapper .more-wrapper{
  position: absolute;
  /* background: yellowgreen; */
  width: 104px;
  height: 31px;
  line-height: 31px;
  right: 0;
  top: 0;
}
.top-wrapper .more-wrapper .spelling-bt{
  color: white;
  width: 30px;
  height: 17px;
  font-size: 10px;
  text-align: center;
  line-height: 17px;
  text-decoration: none;
  border: 1px solid white;
  float: left;
  margin-top: 6px;
  margin-left: 16px;
}
.top-wrapper .more-wrapper .more-bt{
  width: 15px;
  height: 10px;
  float: left;
  margin-left: 15px;
  margin-top: 13px;
}
.top-wrapper .more-wrapper .more-bt .s-radius{
  width: 3px;
  height: 3px;
  border: 1px solid white;
  border-radius: 50%;
  float: left;
}

/* 背景图片样式 */
.bg-wrapper{
  width: 100%;
  height: 150px;
  position: absolute;
  left: 0;
  top: 0;
  z-index: -1;
  background-size: 100% 135%;
  background-position: center -12px;
}

/* 主题内容样式 */
header .content-wrapper{
  height: 50px;
  padding: 17px 10px 11px;
}
.content-wrapper .icon{
  width: 50px;
  height: 50px;
  background-size: 135% 100%;
  background-position: center;
  border-radius: 5px;
  float: left;
}
.content-wrapper .name{
  float: left;
  padding: 18px 0 0 12px;
}
.content-wrapper .name h3{
  font-size: 16px;
  font-weight: bold;
  color: white;
}
.content-wrapper .collect{
  width: 25px;
  height: 37px;
  float: right;
  text-align: center;
  padding-top: 6px;
}
.content-wrapper .collect img{
  width: 20px;
  height: 20px;
}
.content-wrapper .collect span{
  color: white;
  font-size: 12px;
}

/* 公共内容样式 */
header .bulletin-wrapper{
  padding: 0 10px;
}
.bulletin-wrapper img{
  width: 16px;
  height: 16px;
  float: left;
  margin-right: 6px;
}
.bulletin-wrapper .text{
  float: left;
  color: white;
  font-size: 11px;
  line-height: 16px;
}
.bulletin-wrapper .detail{
  float: right;
  font-size: 11px;
  color: white;
  line-height: 16px;
}
.bulletin-wrapper .detail span{
  line-height: 16px;
  font-size: 16px;
  float: right;
}

/* 公告详情样式 */
header .bulletin-detail{
  width: 100vw;
  height: 100vh;
  position: absolute;
  left: 0;
  top: 0;
  z-index: 999;
  background: rgba(98, 98, 98, 0.8);
}
.bulletin-detail .detail-wrapper{
  width: 100%;
  height: 100%;
  padding: 43px 20px 125px;
  box-sizing: border-box;
}
.bulletin-detail .detail-wrapper .main-wrapper{
  width: 100%;
  height: 100%;
  background-size: 100% 100%;
  border-radius: 10px;
  text-align: center;
}
.bulletin-detail .detail-wrapper .main-wrapper .icon{
  width: 60px;
  height: 60px;
  background-size: 135% 100%;
  background-position: center;
  margin-top: 40px;
  border-radius: 5px;
  display: inline-block;
}
.bulletin-detail .detail-wrapper .main-wrapper .name{
  font-size: 15px;
  margin-top: 13px;
  color: white;
}
.bulletin-detail .detail-wrapper .main-wrapper .score{
  height: 10px;
  margin-top: 6px;
  text-align: center;
  font-size: 0;
}
.bulletin-detail .detail-wrapper .main-wrapper .score .star{
  display: inline-block;
  margin-right: 7px;
}
.bulletin-detail .detail-wrapper .main-wrapper .score span{
  display: inline-block;
  color: white;
  font-size: 10px;
}
.bulletin-detail .detail-wrapper .main-wrapper .tip{
  font-size: 11px;
  color: #bababc;
  margin-top: 8px;
}
.bulletin-detail .detail-wrapper .main-wrapper .tip i{
  margin: 0 7px;
}
.bulletin-detail .detail-wrapper .main-wrapper .time{
  font-size: 11px;
  color: #bababc;
  margin-top: 13px;
}
.bulletin-detail .detail-wrapper .main-wrapper .discounts{
  margin-top: 20px;
  padding: 0 20px;
}
.bulletin-detail .detail-wrapper .main-wrapper .discounts p{
  padding-top: 20px;
  border-top: 1px solid #BABABA;
}
.bulletin-detail .detail-wrapper .main-wrapper .discounts img{
  width: 16px;
  height: 16px;
  vertical-align: middle;
}
.bulletin-detail .detail-wrapper .main-wrapper .discounts span{
  font-size: 12px;
  height: 16px;
  line-height: 16px;
  color: white;
}
.bulletin-detail .detail-wrapper .close-wrapper{
  width: 100%;
  height: 30px;
  padding-top: 20px;
  text-align: center;
}
.bulletin-detail .detail-wrapper .close-wrapper span{
  width: 40px;
  height: 40px;
  line-height: 40px;
  border-radius: 50%;
  font-size: 14px;
  color: white;
  display: inline-block;
  background: rgba(118, 118, 118, 0.7);
  border: 1px solid rgba(140, 140, 140, 0.9);
}

/* 动画效果 */ 
.bulletin-detail-enter-active,
.bulletin-detail-leave-active {
  transition: 2s all;
}

.bulletin-detail-enter,
.bulletin-detail-leave-to {
  opacity: 0;
}

.bulletin-detail-enter-to,
.bulletin-detail-leave {
  opacity: 1;
}
</style>
