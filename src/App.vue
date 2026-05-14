<script setup>
import { RouterView } from 'vue-router'
import { ref, onMounted } from 'vue'

// 你的必应壁纸逻辑保持不变
const bingBg = ref('')
const bingTitle = ref('')
const bingCopyright = ref('')

const fetchBingWallpaper = async () => {
  try {
    const res = await fetch('https://www.bing.com/HPImageArchive.aspx?format=js&idx=0&n=1')
    const data = await res.json()
    if (data.images && data.images.length > 0) {
      bingBg.value = 'https://www.bing.com' + data.images[0].url
      bingTitle.value = data.images[0].copyright
      bingCopyright.value = data.images[0].copyrightlink
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
  <!-- 
    1. 根容器：relative 定位，用于控制子元素层级 
    2. 关键：这里绝对不能写 background-color: white
  -->
  <div class="app-container">
    
    <!-- 层级 1: 背景图 (最底层) -->
    <div class="background-image" v-if="bingBg">
      <img :src="bingBg" alt="Bing Wallpaper" />
    </div>

    <!-- 层级 2: 路由内容 (TheDoc.vue 会在这里渲染) -->
    <!-- TheDoc.vue 自带了 ::before 遮罩，所以这里不需要额外的遮罩 -->
    <div class="main-content">
      <RouterView />
    </div>
    
  </div>
</template>

<style scoped>
/* 根容器占满全屏 */
.app-container {
  position: relative;
  width: 100vw;
  min-height: 100vh;
  /* 确保没有白色背景 */
  background-color: transparent; 
  overflow: hidden; /* 防止滚动条干扰 */
}

/* 背景图样式 */
.background-image {
  position: fixed; /* 固定定位，防止滚动时背景移动 */
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1; /* 强制在最底层 */
  overflow: hidden;
}

.background-image img {
  width: 100%;
  height: 100%;
  object-fit: cover; /* 图片覆盖全屏 */
}

/* 内容区域 */
.main-content {
  position: relative;
  z-index: 1; /* 确保内容在背景图之上 */
  /* 注意：不要在这里设置背景色，让 TheDoc.vue 控制 */
}
</style>
