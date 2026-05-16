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
    bingBg.value = `https://www.bing.com${img.urlBase}_UHD.jpg` // 使用高清大图
    bingTitle.value = img.title
    bingCopyright.value = img.copyright
  } catch (error) {
    console.error('获取壁纸失败:', error)
  }
}

onMounted(() => {
  fetchBingWallpaper()
})
</script>

<template>
  <div class="app-container">
    <!-- 1. 背景层：固定在底部 -->
    <div 
      class="background-layer" 
      v-if="bingBg"
      :style="{ backgroundImage: `url(${bingBg})` }"
    ></div>

    <!-- 2. 内容层：显示你的图标和路由视图 -->
    <div class="content-layer">
      <RouterView />
    </div>
  </div>
</template>

<style scoped>
.app-container {
  position: relative;
  min-height: 100vh;
  width: 100%;
  overflow: hidden; /* 防止背景图溢出出现滚动条 */
}

/* 背景层样式 */
.background-layer {
  position: fixed; /* 固定定位，随屏幕滚动 */
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-size: cover;
  background-position: center;
  z-index: -1; /* 放在最底层 */
  filter: blur(8px); /* 磨砂模糊效果 */
  transform: scale(1.1); /* 放大一点防止模糊后露边 */
}

/* 遮罩层：让文字更清晰（可选） */
.background-layer::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.4); /* 黑色半透明遮罩，加深背景 */
  z-index: 0;
}

/* 内容层样式 */
.content-layer {
  position: relative;
  z-index: 10; /* 确保内容在背景之上 */
  min-height: 100vh;
}
</style>
