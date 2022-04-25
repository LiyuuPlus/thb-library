<template>
  <el-config-provider :locale="lang">
    <el-container>
      <el-header>
        <NavBar />
      </el-header>
      <el-main>
        <RouterView />
      </el-main>
      <el-footer>

      </el-footer>
    </el-container>
  </el-config-provider>
</template>
<script lang="ts" setup>
import zhCn from 'element-plus/lib/locale/lang/zh-cn';
import NavBar from './components/NavBar.vue';
const lang = zhCn;
</script>

<style>
#app {}
</style>
