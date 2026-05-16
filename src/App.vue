<script setup>
import { RouterView } from 'vue-router'
import { ref, onMounted } from 'vue'

const bingBg = ref('')

const fetchBingWallpaper = async () => {
  try {
    const res = await fetch('https://www.bing.com/HPImageArchive.aspx?format=js&idx=0&n=1&mkt=zh-CN')
    const data = await res.json()
    const img = data.images[0]
    bingBg.value = `https://www.bing.com${img.urlBase}_UHD.jpg`
  } catch (e) {
    bingBg.value = 'https://picsum.photos/1920/1080?random=1'
  }
}

onMounted(fetchBingWallpaper)
</script>

<template>
  <!-- Bing 背景 -->
  <div class="fixed inset-0 bg-cover bg-center bg-no-repeat -z-10" 
       :style="{ backgroundImage: `url(${bingBg})` }"></div>
  
  <!-- 简单暗色遮罩 -->
  <div class="fixed inset-0 bg-black/20 -z-9"></div>

  <!-- 主要内容 - 强制最高层级 -->
  <RouterView class="relative z-50" />
</template>
