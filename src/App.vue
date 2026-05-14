<script setup>
import { RouterView } from 'vue-router'
import { ref, onMounted } from 'vue'

const bingBg = ref('')
const bingTitle = ref('')
const bingCopyright = ref('')

// 获取必应壁纸
const fetchBingWallpaper = async () => {
  try {
    const res = await fetch('https://www.bing.com/HPImageArchive.aspx?format=js&idx=0&n=1')
    const data = await res.json()
    if (data.images && data.images.length > 0) {
      bingBg.value = 'https://www.bing.com' + data.images[0].url
      bingTitle.value = data.images[0].copyright
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
  <!-- 1. 背景图层：固定在底层 -->
  <div class="bg-container" v-if="bingBg">
    <img :src="bingBg" class="bg-image" alt="background" />
    <!-- 可选：如果不想让 TheDoc 的遮罩太黑，可以在这里加一层朦胧感 -->
    <!-- <div class="bg-overlay"></div> -->
  </div>

  <!-- 2. 内容层：TheDoc 和 路由视图 -->
  <!-- 注意：这里不需要额外的包裹 div，直接放 RouterView，TheDoc 在路由里 -->
  <RouterView />
</template>

<style scoped>
/* 背景容器：固定定位，铺满全屏，层级最低 */
.bg-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  z-index: -1; /* 关键：放在最底下 */
  overflow: hidden;
}

/* 背景图片样式 */
.bg-image {
  width: 100%;
  height: 100%;
  object-fit: cover; /* 保持比例铺满 */
}

/* 如果你想在图片上加一层模糊或变暗，可以用这个类 */
/*
.bg-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.2);
}
*/
</style>
