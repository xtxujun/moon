<script setup>
import { RouterView } from 'vue-router'
import { ref, onMounted } from 'vue'

const bingBg = ref('')
const bingTitle = ref('')
const bingCopyright = ref('')

const fetchBingWallpaper = async () => {
  try {
    const res = await fetch('https://www.bing.com/HPImageArchive.aspx?format=js&idx=0&n=1&mkt=zh-CN')
    const data = await res.json()
    const img = data.images[0]
    bingBg.value = `https://www.bing.com${img.urlBase}_UHD.jpg`
    bingTitle.value = img.title || 'Bing 每日美图'
    bingCopyright.value = img.copyright || ''
  } catch (e) {
    bingBg.value = 'https://picsum.photos/1920/1080?random=1'
  }
}

onMounted(() => {
  fetchBingWallpaper()
  setInterval(fetchBingWallpaper, 86400000)
})
</script>

<template>
  <!-- Bing 背景 -->
  <div 
    class="fixed inset-0 bg-cover bg-center bg-no-repeat -z-10 transition-all duration-1000"
    :style="{ backgroundImage: `url(${bingBg})` }"
  ></div>

  <!-- 白色磨砂毛玻璃 - 较轻版 -->
<div class="fixed inset-0 bg-white/35 dark:bg-black/55 backdrop-blur-[6px] -z-9"></div>

  <!-- 图片信息 -->
  <div v-if="bingTitle" class="fixed bottom-6 right-6 text-white/90 dark:text-white/80 text-right z-10 max-w-xs pointer-events-none drop-shadow-md">
    <div class="text-sm">{{ bingTitle }}</div>
    <div class="text-xs opacity-75">{{ bingCopyright }}</div>
  </div>

  <RouterView />
</template>
