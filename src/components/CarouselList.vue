<template>
    <el-carousel indicator-position="outside" :height="imgHeight + 'px'">
        <el-carousel-item v-for="(carousel, index) in list" :key="index">
            <el-image :src="carousel.pic" />
        </el-carousel-item>
    </el-carousel>
</template>
<script lang="ts" setup>
import { getCurrentInstance, onMounted, ref, watch } from "vue";
import { CarouselItem } from "../models/home";

const props  = defineProps<{ list: CarouselItem[],width?:Number,height?:Number }>();

const { proxy } = getCurrentInstance();
const imgHeight = ref(0);
const screenWidth = ref(0);
const timer = ref(false);

const setSize = () => {
    const bit =props.width && props.height ? props.height / props.width : 300 / 1440;
    imgHeight.value = bit * screenWidth.value;
}

onMounted(() => {
    screenWidth.value = proxy.$el.clientWidth;
    window.addEventListener('resize', () => {
        screenWidth.value = proxy.$el.clientWidth;
    })
});

watch(screenWidth, (newVal) => {
    if (!timer.value) {
        screenWidth.value = newVal;
        timer.value = true;
        setTimeout(() => {
            setSize();
            timer.value = false;
        }, 200)
    }
})

</script>
<style lang="less">
.el-carousel__container {
    transition: all 300ms ease 0ms;
    .el-carousel__item {
        .el-image {
            width: 100%;
        }
    }
}
</style>