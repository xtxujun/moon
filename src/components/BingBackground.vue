<template>
  <div class="bing-bg">
    <!-- 背景图：加载 Bing 图片 -->
    <img :src="imageUrl" class="bg-img" alt="bing-bg" />

    <!-- 遮罩层：增加暗色滤镜，保证前景文字清晰可见 -->
    <div class="bg-mask"></div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

const imageUrl = ref('')

onMounted(() => {
  // 请求 Bing 每日图片接口
  fetch('https://www.bing.com/HPImageArchive.aspx?format=js&idx=0&n=1&mkt=zh-CN')
    .then(res => res.json())
    .then(data => {
      if (data.images && data.images.length > 0) {
        // 拼接完整图片地址
        imageUrl.value = 'https://www.bing.com' + data.images[0].url
      }
    })
    .catch(err => {
      console.error('Bing 壁纸获取失败', err)
    })
})
</script>

<style scoped>
.bing-bg {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  z-index: -1; /* 确保背景在最底层 */
  overflow: hidden;
}

.bg-img {
  width: 100%;
  height: 100%;
  object-fit: cover; /* 图片铺满且不变形 */
  /* 核心代码：毛玻璃模糊效果 */
  filter: blur(20px) brightness(0.8);
  transform: scale(1.1); /* 放大一点防止模糊后边缘露白 */
}

.bg-mask {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  /* 叠加一层黑色半透明，让上面的白色文字更清晰 */
  background: rgba(0, 0, 0, 0.2);
}
</style>
