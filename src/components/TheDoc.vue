<template>
  <!-- 
       关键点：
       1. relative: 相对定位
       2. min-h-screen: 最小高度占满屏幕
       3. bg-cover/center: 背景图覆盖全屏
       4. 这里的 style 绑定了 bingBg 
  -->
  <div 
    class="relative min-h-screen bg-cover bg-center overflow-hidden"
    :style="{ backgroundImage: `url(${bingBg})` }"
  >
    <!-- 遮罩层（可选）：让文字更清晰 -->
    <div class="absolute inset-0 bg-black/20 backdrop-blur-[2px]"></div>

    <!-- 内容插槽 -->
    <div class="relative z-10 flex flex-col min-h-screen">
      <slot />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

const bingBg = ref('')

// 获取必应壁纸
const fetchBingWallpaper = async () => {
  try {
    const res = await fetch('https://www.bing.com/HPImageArchive.aspx?format=js&idx=0&n=1')
    const data = await res.json()
    if (data.images && data.images.length > 0) {
      bingBg.value = 'https://www.bing.com' + data.images[0].url
    }
  } catch (error) {
    console.error('获取壁纸失败', error)
  }
}

onMounted(() => {
  fetchBingWallpaper()
})
</script>
