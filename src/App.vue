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
  <div class="fixed inset-0 bg-cover bg-center -z-10" :style="{ backgroundImage: `url(${bingBg})` }"></div>
  <div class="fixed inset-0 bg-black/30 -z-9"></div>   <!-- 临时简单叠加 -->
  <RouterView />
</template>
