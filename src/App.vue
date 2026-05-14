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
    
    bingBg.value = `https://www.bing.com${img.urlbase}_UHD.jpg`
    bingTitle.value = img.title
    bingCopyright.value = img.copyright
  } catch (e) {
    console.error('Bing 背景加载失败，使用备用图')
    bingBg.value = 'https://picsum.photos/1920/1080?random=42'
  }
}

onMounted(fetchBingWallpaper)
</script>

<template>
  <!-- 1. 背景图层 (最底层) -->
  <div 
    class="fixed inset-0 bg-cover bg-center bg-no-repeat -z-10"
    :style="{ backgroundImage: `url(${bingBg})` }"
  ></div>

  <!-- 2. 磨砂玻璃层 (中间层) -->
  <!-- 注意：backdrop-blur 是实现毛玻璃的关键，bg-black/40 是半透明黑色背景 -->
  <div class="fixed inset-0 bg-black/40 backdrop-blur-3xl -z-9"></div>

  <!-- 3. 图片信息 (文字层) -->
  <!-- pointer-events-none 让这个文字层不阻挡下方的点击事件 -->
  <div v-if="bingTitle" class="fixed bottom-4 right-4 text-white/90 text-sm max-w-xs text-right z-10 pointer-events-none">
    <div class="font-medium">{{ bingTitle }}</div>
    <div class="text-xs opacity-80 text-ellipsis overflow-hidden whitespace-nowrap">
      {{ bingCopyright }}
    </div>
  </div>

  <!-- 4. 应用内容 (最上层) -->
  <!-- 这里的内容会显示在磨砂层和背景图之上 -->
  <AppProvider>
    <AppContainer>
      <RouterView />
    </AppContainer>
  </AppProvider>
</template>

<style scoped>
/* 
  backdrop-blur 兼容性处理 (如果部分浏览器不生效可尝试开启 autoprefixer)
  这里设置毛玻璃的模糊程度，blur-3xl 是非常强的模糊，看起来像磨砂质感
*/
</style>
