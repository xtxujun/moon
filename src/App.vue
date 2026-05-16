<script setup>
import { RouterView } from 'vue-router'
import { ref, onMounted } from 'vue'

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
  <!-- 1. 背景层：强制沉底，且禁止鼠标事件（让点击穿透到下层） -->
  <div 
    class="fixed inset-0 w-full h-full bg-cover bg-center z-[-1] pointer-events-none select-none"
    :style="{ backgroundImage: 'url(' + bingBg + ')' }"
  ></div>

  <!-- 2. 内容层：不需要额外的包裹，直接渲染路由 -->
  <!-- 注意：这里不要加任何背景色或z-index -->
  <RouterView />
</template>
