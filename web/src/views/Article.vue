<template>
  <div class="page-article" v-if="model">
    <div class="d-flex py-3 px-2 border-bottom">
      <div class="iconfont icon-Back text-blue"></div>
      <strong class="flex-1 text-blue pl-2">
        {{model.title}}
      </strong>
      <div class="text-gray fs-xs">
        2020-08-11
      </div>
    </div>
    <div v-html="model.body" class="px-3 body fs-lg"></div>
    <div class="px-3 border-top py-3">
      <div class="d-flex ai-center">
        <i class="iconfont icon-menu"></i>
        <span class="text-blue fs-lg ml-1">相关资讯</span>
      </div>
      <div class="pt-2">
        <router-link tag="div" 
        class="py-1"
        :to="`/articles/${item._id}`"
        v-for="item in model.related" 
        :key="item._id">
          {{item.title}}
        </router-link>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    id: { required: true }
  },
  data() {
    return {
      model: null
    }
  },
  methods: {
    async fetch(){
      const res = await this.$http.get(`articles/${this.id}`)
      this.model = res.data
    }
  },
  watch: {
    id: 'fetch'
    // id(){
    //   this.fetch()
    // }
  },
  created() {
    this.fetch()
  }
}
</script>

<style lang="scss">
.page-article{
  .icon-Back{
    font-size: 1rem;
  }
  .body{
    img{
      max-width: 100%;
      height: auto;
    }
    iframe{
      width: 100%;
      height: auto;
    }
  }
}
</style>