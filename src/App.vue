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
  <div class="fixed inset-0 bg-cover bg-center -z-10" :style="{ backgroundImage: `url(${bingBg})` }"></div>
  
  <!-- 白色磨砂 -->
  <div class="fixed inset-0 bg-white/35 dark:bg-black/60 backdrop-blur-[8px] -z-9"></div>

  <!-- 内容强制最高层级 -->
  <RouterView class="relative z-[9999]" />
</template>
