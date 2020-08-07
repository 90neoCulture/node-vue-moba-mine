<template>
  <div>
    <swiper :options="swiperOption" ref="mySwiper">
      <!-- slides -->
      <swiper-slide>
        <img class="w-100" src="../assets/images/ec5d03bcf94642594b8f0beb49b5f61c.jpeg" alt="">
      </swiper-slide>
      <swiper-slide>
        <img class="w-100" src="../assets/images/8025f865e900cb0f2acd59e2ad5ff2f2.jpeg" alt="" srcset="">
      </swiper-slide>
      <swiper-slide>
        <img class="w-100" src="../assets/images/f801359d7c1d8b6fae518a99c59670ec.jpeg" alt="">
      </swiper-slide>
      <!-- Optional controls -->
      <div class="swiper-pagination pagination-home text-right px-3 pb-1"
        slot="pagination">
      </div>
    </swiper>
    <!-- end of swiper -->
    <div class="nav-icons bg-white mt-3 text-center pt-3 text-dark-1">
      <div class="d-flex flex-wrap">
        <div class="nav-item mb-3" v-for="n in 10" :key="n">
          <i class="sprite sprite-news"></i>
          <div class="py-2">爆料站</div>
        </div>
      </div>
      <div class="bg-light py-2 fs-sm">
        <i class="sprite sprite-arrow mr-1"></i>
        <span>收起</span>
      </div>
    </div>
    <!-- end of nav icons -->
    <!-- <m-card icon="menu" title="新闻资讯"> -->
      <m-list-card icon="menu" title="新闻资讯" :categories="newsCats">
        <template #items="{ category }">
          <div class="py-2" v-for="(news, nIndex) in category.newsList" :key="nIndex">
            <span>[{{news.categoryName}}]</span>
            <span>|</span>
            <span>{{news.title}}</span>
            <span>{{news.date}}</span>
          </div>
        </template>
      </m-list-card>
    <!-- </m-card> -->
    <i class="iconfont icon-menu text-primary"></i>
  </div>
</template>

<script>
export default {
    name: 'carrousel',
    data() {
      return {
        swiperOption: {
          pagination: {
            el: ".pagination-home"
          }
        },
        newsCats: [
          {
          name: '热门',
          newsList: new Array(5).fill(1).map(() => ({
              categoryName: '公告',
              title: '8月6日体验服停机更新公告',
              date: '08/06'
            }))
        },{
          name: '新闻',
          newsList: new Array(5).fill(1).map(() => ({
              categoryName: '公告',
              title: '8月6日体验服停机更新公告',
              date: '08/06'
            }))
        },{
          name: '公告',
          newsList: new Array(5).fill(1).map(() => ({
              categoryName: '公告',
              title: '8月6日体验服停机更新公告',
              date: '08/06'
            }))
        },{
          name: '活动',
          newsList: new Array(5).fill(1).map(() => ({
              categoryName: '公告',
              title: '8月6日体验服停机更新公告',
              date: '08/06'
            }))
        },{
          name: '赛事',
          newsList: new Array(5).fill(1).map(() => ({
              categoryName: '公告',
              title: '8月6日体验服停机更新公告',
              date: '08/06'
            }))
        },]
          
      }
    },
    computed: {
      swiper() {
        return this.$refs.mySwiper.swiper
      }
    },
    mounted() {
      
    }
  }
</script>
<style lang="scss">
@import '../assets/scss/_variables.scss';
.pagination-home{
  .swiper-pagination-bullet{
    opacity: 1;
    border-radius: 0.1538rem;
    background: map-get($colors, 'white');
    &.swiper-pagination-bullet-active{
      background: map-get($colors, 'info');
    }
  }
}
.nav-icons{
  border-top: 1px solid $border-color;
  border-bottom: 1px solid $border-color;
  .nav-item {
    width: 25%;
    border-left: 1px solid $border-color;
    &:nth-child(4n+1){
      border-left: none;
    }
  }
}
</style>
