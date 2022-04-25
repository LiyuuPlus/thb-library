<template>
<CarouselList  :list="carouselList"/>
  <el-row :gutter="20">
    <el-col :span="16" :sm="16" :xs="24">
      <div class="grid-content bg-purple" />
    </el-col>
    <el-col :span="8" class="hidden-xs">
      <div class="grid-content bg-purple" />
    </el-col>
  </el-row>
</template>
<script lang="ts" setup>
import 'element-plus/theme-chalk/display.css'
import { ref } from 'vue';
import { CarouselItem } from '../models/home';
import CarouselList from '../components/CarouselList.vue';

// 变量
const carouselList = ref<CarouselItem[]>([]);

// 方法
const getCarousels = () => {
  const data: CarouselItem[] = [
    {
      name: "首页",
      pic: "https://www.alicem.top/usr/themes/blogimg/52442920_p0.jpg",
      url: '/home'
    },
  ];
  carouselList.value = data;
}

// 执行
getCarousels();

</script>
<style lang="less">
.grid-content {
  border-radius: 4px;
  min-height: 500px;
}

.bg-purple {
  --un-bg-opacity: 1;
  background-color: rgba(192, 132, 252, var(--un-bg-opacity));
}
</style>