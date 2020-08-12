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
    <m-list-card icon="menu" title="新闻资讯" :categories="newsCats">
      <template #items="{ category }">
        <router-link 
        tag="div"
        :to="`/articles/${news._id}`"
        class="py-2 fs-lg d-flex" 
        v-for="(news, nIndex) in category.newsList" :key="nIndex">
          <span>[{{news.categoryName}}]</span>
          <span class="px-2">|</span>
          <span class="flex-1 text-dark-1 text-ellipsis pr-2">{{news.title}}</span>
          <span class="text-gray-1 fs-sm">{{news.createdAt | date}}</span>
        </router-link>
      </template>
    </m-list-card>
    <m-list-card icon="card-hero" title="英雄列表" :categories="heroCats">
      <template #items="{ category }">
        <div class="d-flex flex-wrap" style="margin: 0 -0.5rem;">
          <router-link 
          tag="div"
          :to="`/heroes/${hero._id}`"
          class="p-2 text-center" 
          style="width: 20%;"
          v-for="(hero, nIndex) in category.heroList" :key="nIndex">
            <img :src="hero.avatar" alt="" class="w-100">
            <div>{{hero.name}}</div>
          </router-link>
        </div>
      </template>
    </m-list-card>
  </div>
</template>

<script>
import dayjs from 'dayjs'
export default {
    name: 'carrousel',
    data() {
      return {
        swiperOption: {
          pagination: {
            el: ".pagination-home"
          }
        },
        newsCats: [],
        heroCats: []
      }
    },
    filters: {
      date(val){
        return dayjs(val).format('MM/DD')
      }
    },
    created() {
      this.fetchNewCats()
      this.fetchHeroCats()
    },
    methods: {
      async fetchNewCats(){
        const res = await this.$http.get('/news/list')
        this.newsCats = res.data
      },
      async fetchHeroCats(){
        const res = await this.$http.get('/heroes/list')
        this.heroCats = res.data
      }
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
