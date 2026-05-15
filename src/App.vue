<script setup>
import { RouterView } from 'vue-router'
import { ref, onMounted } from 'vue'

const bingBg = ref('')
const bingTitle = ref('')
const bingCopyright = ref('')

const fetchBingWallpaper = async () => {
  try {
    // 官方 Bing API（每日更新）
    const res = await fetch('https://www.bing.com/HPImageArchive.aspx?format=js&idx=0&n=1&mkt=zh-CN')
    const data = await res.json()
    const img = data.images[0]
    
    bingBg.value = `https://www.bing.com${img.urlBase}_UHD.jpg`
    bingTitle.value = img.title
    bingCopyright.value = img.copyright
  } catch (e) {
    console.error('Bing 背景加载失败，使用备用图')
    bingBg.value = 'https://picsum.photos/1920/1080?random=42'
  }
}

onMounted(fetchBingWallpaper)
</script>

<template>
  <!-- Bing 动态背景 -->
  <div 
    class="fixed inset-0 bg-cover bg-center bg-no-repeat -z-10 transition-all duration-1000"
    :style="{ backgroundImage: `url(${bingBg})` }"
  ></div>

  <!-- 【修改这里】白色系毛玻璃叠加层 -->
  <div class="fixed inset-0 bg-white/40 dark:bg-black/50 backdrop-blur-[6px] -z-9"></div>

  <!-- 图片信息 -->
  <div v-if="bingTitle" class="fixed bottom-6 right-6 text-white/90 dark:text-white/80 text-right z-10 max-w-xs pointer-events-none drop-shadow-md">
    <div class="text-sm">{{ bingTitle }}</div>
    <div class="text-xs opacity-75">{{ bingCopyright }}</div>
  </div>

  <RouterView />
</template>

<style scoped>
/* 可根据需要调整毛玻璃强度 */
</style>
