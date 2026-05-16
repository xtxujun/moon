<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { useSettingStore } from '@/stores/setting' // 确保这个路径正确

// 模拟组件逻辑，直接写在页面里，避免文件缺失报错
const settingStore = useSettingStore()

// 壁纸逻辑
const bingBg = ref('')
const fetchBingWallpaper = async () => {
  try {
    const res = await fetch('https://www.bing.com/HPImageArchive.aspx?format=js&idx=0&n=1')
    const data = await res.json()
    if (data.images && data.images.length > 0) {
      bingBg.value = 'https://www.bing.com' + data.images[0].url
    }
  } catch (error) {
    console.error(error)
  }
}

onMounted(() => {
  fetchBingWallpaper()
})
</script>

<template>
  <!-- 1. 背景层：固定在底层 -->
  <div 
    v-if="bingBg"
    class="fixed inset-0 w-full h-full bg-cover bg-center z-[-1] transition-all duration-1000"
    :style="{ backgroundImage: `url(${bingBg})` }"
  >
    <!-- 黑色遮罩，让文字更清晰 -->
    <div class="absolute inset-0 bg-black/20 backdrop-blur-[2px]"></div>
  </div>

  <!-- 2. 内容层：磨砂玻璃效果 -->
  <div class="relative z-[100] min-h-screen flex flex-col items-center justify-center p-4 sm:p-8">
    
    <!-- 主容器：这里是核心，使用 bg-white/30 实现透明白 -->
    <div class="w-full max-w-2xl bg-white/30 dark:bg-zinc-900/30 backdrop-blur-xl border border-white/40 dark:border-zinc-700/40 rounded-3xl shadow-2xl overflow-hidden transition-all duration-300">
      
      <!-- 头部区域 -->
      <div class="p-8 pb-4 text-center">
        <h1 class="text-3xl font-bold text-gray-800 dark:text-gray-100 mb-2">
          欢迎回来
        </h1>
        <p class="text-gray-600 dark:text-gray-400">
          {{ new Date().toLocaleDateString() }}
        </p>
      </div>

      <!-- 时钟区域 (模拟 MainClock) -->
      <div class="py-8 text-center">
        <div class="text-6xl font-mono font-bold text-gray-800 dark:text-gray-100 tracking-wider">
          {{ new Date().getHours() }}:{{ String(new Date().getMinutes()).padStart(2, '0') }}
        </div>
      </div>

      <!-- 搜索区域 (模拟 MainSearch) -->
      <div class="px-8 pb-8">
        <div class="relative group">
          <input 
            type="text" 
            placeholder="输入搜索内容..." 
            class="w-full h-12 pl-12 pr-4 bg-white/60 dark:bg-zinc-800/60 border-none rounded-full shadow-inner focus:ring-2 focus:ring-blue-400 text-gray-800 dark:text-gray-100 placeholder-gray-500 transition-all"
          />
          <div class="absolute left-4 top-3.5 text-gray-400">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
            </svg>
          </div>
