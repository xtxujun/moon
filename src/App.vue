<script setup>
import { RouterView } from 'vue-router'
import { ref, onMounted } from 'vue'

const bingBg = ref('')

const fetchBingWallpaper = async () => {
  try {
    // 获取必应每日一图
    const res = await fetch('https://www.bing.com/HPImageArchive.aspx?format=js&idx=0&n=1')
    const data = await res.json()
    if (data.images && data.images.length > 0) {
      bingBg.value = 'https://www.bing.com' + data.images[0].url
    }
  } catch (error) {
    console.error('获取壁纸失败:', error)
  }
}

onMounted(() => {
  fetchBingWallpaper()
})
</script>

<template>
  <!-- 背景层：强制固定在底层 -->
  <div 
    class="fixed inset-0 w-full h-full bg-cover bg-center z-[-1] transition-all duration-500"
    :style="{ backgroundImage: bingBg ? 'url(' + bingBg + ')' : 'none' }"
  ></div>

  <!-- 内容层 -->
  <RouterView />
</template>
