<script setup lang="ts">
import MainHeader from '@/components/MainHeader.vue'
import MainClock from '@/components/MainClock.vue'
import MainSearch from '@/components/MainSearch.vue'
import SiteContainer from '@/components/SiteContainer.vue'
import MainSetting from '@/components/MainSetting.vue'
import TheFooter from '@/components/TheFooter.vue' // 假设你有这个组件

// 假设你使用了 Pinia
import { useSettingStore } from '@/stores/setting' 

const settingStore = useSettingStore()
</script>

<template>
  <!-- TheDoc 包裹层 -->
  <TheDoc>
    
    <!-- 核心卡片容器 -->
    <!-- 
      关键修改：
      1. 移除了 bg="$main-bg-c"
      2. 使用 bg-white/40 (40% 透明度)
      3. 添加 backdrop-blur-xl (磨砂效果)
      4. 添加 border (边框增加质感)
    -->
    <div class="relative z-[10000] min-h-screen p-12 sm:p-24 flex flex-col items-center">
      
      <!-- 顶部导航 -->
      <MainHeader class="w-full mb-8" />

      <!-- 时钟组件 -->
      <MainClock v-if="settingStore.isSetting" class="mb-8" />

      <!-- 搜索组件 -->
      <MainSearch v-if="settingStore.isSetting" class="my-24 w-full max-w-2xl" />

      <!-- 网站容器 -->
      <SiteContainer :key="settingStore.siteContainerKey" class="w-full flex-1" />

      <!-- 设置入口 -->
      <MainSetting class="mt-8" />

      <!-- 底部 -->
      <TheFooter v-if="settingStore.getSettingValue('showFooter')" class="mt-auto pt-8" />
      
    </div>
  </TheDoc>
</template>
