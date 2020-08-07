<template>
  <m-card :icon="icon" :title="title">
    <div class="nav jc-between">
      <div class="nav-item" v-for="(category, i) in categories" :key="i" :class="{active: active == i}" @click="active = i">
        <div class="nav-link">{{category.name}}</div>
      </div>
    </div>
    <div class="pt-3">
      <swiper>
        <swiper-slide v-for="(category,i) in categories" :key="i">
          <slot name="items" :category="category"></slot>
        </swiper-slide>
      </swiper>
    </div>
  </m-card>
</template>

<script>
export default {
  data() {
    return {
      active: 0
    }
  },
  props: {
    icon: {type: String, required: true},
    title: {type: String, required: true},
    categories: {type: Array, required: true}
  }
}
</script>