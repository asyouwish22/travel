<template>
  <div class="icons">
    <swiper :options="swiperOption">
      <swiper-slide v-for="(page,index) of pages" :key="index">
        <div class="icon" v-for="item of page" :key="item.id">
          <div class="icon-img">
            <img
              :src='item.imgUrl'
              alt=""
            />
          </div>
          <p class="icon-desc">{{item.desc}}</p>
        </div>
      </swiper-slide>
    </swiper>
  </div>
</template>

<script>
import { swiper, swiperSlide } from "vue-awesome-swiper";
import "swiper/dist/css/swiper.css";
export default {
  name: "Icons",
  props:{
    iconList:Array
  },
  data() {
    return {
      swiperOption: {
        loop: true,
      },
    };
  },
  components: {
    swiper,
    swiperSlide,
  },
  computed: {
    pages(){
      const pages=[];
      this.iconList.forEach((item,index)=>{
        // 计算图标应该出现在第几页
        const page=Math.floor(index/8);
        // 将每一页图标初始化成为一个空数组
        if(!pages[page]){
          pages[page]=[]
        }
        // pages为二维数组，
        pages[page].push(item)
      })
      return pages
    }
  },
};
</script>

<style lang="stylus" scoped>
.icons >>> .swiper-container
  height 0
  padding-bottom 50%
.icons {
  width: 100%;
  // background pink
  height: 0;
  padding-bottom: 50%;
  margin-top :.1rem

  .icon {
    float: left;
    width: 25%;
    // background skyblue
    padding-bottom: 25%;
    position: relative;
    height: 0;

    .icon-img {
      position: absolute;
      top: 0;
      right: 0;
      left: 0;
      bottom: 0.44rem;
      box-sizing: border-box;
      padding: 0.1rem;
    }

    .icon-img img {
      height: 100%;
      margin: 0 auto;
      display: block;
    }

    .icon-desc {
      position: absolute;
      bottom: 0;
      left: 0;
      right: 0;
      color: #333;
      height: 0.44rem;
      line-height: 0.44rem;
      text-align: center;
      font-size: 0.24rem;
      overflow:hidden;
      text-overflow:ellipsis;
      white-space:nowrap
    }
  }
}
</style>