<template>
    <div class="header">
        <div class="sitename">
            幻想乡大图书馆
        </div>
        <div class="menu">
            <el-menu mode="horizontal" :default-active="$route.path" router :ellipsis="false">
                <template v-if="!mobile">
                    <template v-for="(menu) in menuList" :key="menu.index">
                        <el-menu-item v-if="!menu.subMenus" v-text="menu.name" :index="menu.index"></el-menu-item>
                    </template>
                </template>
                <template v-else>
                    <el-sub-menu>
                        <template #title>
                            <el-icon>
                                <fold />
                            </el-icon>
                        </template>
                        <template v-for="(menu) in menuList" :key="menu.index">
                            <el-menu-item v-if="!menu.subMenus" v-text="menu.name" :index="menu.index"></el-menu-item>
                        </template>
                    </el-sub-menu>
                </template>
            </el-menu>
        </div>
    </div>
</template>
<script lang="ts" setup>
import { onMounted, watch } from "vue";
import { ref } from "vue-demi";
import fold from '@element-plus/icons-vue/dist/lib/fold.vue'

interface MenuItem {
    name: String,
    index: String,
    subMenus?: MenuItem[]
}

// 变量
const screenWidth = ref(0);
const menuList = ref<MenuItem[]>([]);
const timer = ref(false);
const mobile = ref(false)

// 方法

const getMenus = () => {
    const data: MenuItem[] = [
        {
            name: "首页",
            index: '/home'
        },
        {
            name: "社团",
            index: '/organization'
        },
        {
            name: "关于我们",
            index: '/about'
        },
        {
            name: "搜索",
            index: '/search'
        },
    ];
    menuList.value = data;
}

// 执行
getMenus();

// 事件
onMounted(() => {
    screenWidth.value = document.body.clientWidth;
    window.addEventListener('resize', () => {
        screenWidth.value = document.body.clientWidth;
    })
});

watch(screenWidth, (newVal) => {
    if (!timer.value) {
        screenWidth.value = newVal;
        timer.value = true;
        setTimeout(() => {
            mobile.value = newVal <= 600;
            timer.value = false;
        }, 200)
    }
});

</script>
<style lang="less">
.header {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    align-content: center;
    justify-content: space-around;
    align-items: baseline;
    height: 100%;

    .sitename {
        padding: 5px;
        font-weight: bold;
        font-size: 1.2rem;
    }
}
</style>