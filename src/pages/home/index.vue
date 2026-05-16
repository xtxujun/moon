<script setup lang="ts">
import { ref, onMounted } from 'vue'
// 【关键修改1】路径必须用 @/ 开头，指向 src/components，不能用 ./components
import MainHeader from '@/components/MainHeader.vue'
import MainClock from '@/components/MainClock.vue'
import MainSearch from '@/components/MainSearch.vue'
import SiteContainer from '@/components/SiteContainer.vue'
import MainSetting from '@/components/MainSetting.vue'
import TheFooter from '@/components/TheFooter.vue'

// 获取 Pinia store
const settingStore = useSettingStore()

// 【关键修改2】Bing 壁纸逻辑
const bingBg = ref('')
const fetchBingWallpaper = async () => {
  try {
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
  <!-- 【关键修改3】背景层：强制固定在屏幕最底层，z-[-1] 确保不挡住内容 -->
  <div 
    class="fixed inset-0 w-full h-full bg-cover bg-center bg-no-repeat z-[-1] transition-opacity duration-1000"
    :style="{ backgroundImage: bingBg ? 'url(' + bingBg + ')' : 'none' }"
  >
    <!-- 可选：加一层黑色半透明遮罩，让图标在亮色壁纸上更清晰 -->
    <div class="absolute inset-0 bg-black/10"></div>
  </div>

  <!-- 内容层 -->
  <TheDoc>
    <!-- 【关键修改4】删除了 bg="$main-bg-c"，改为 bg="transparent" -->
    <div 
      p="12 sm:24" 
      w="full sm:auto" 
      bg="transparent" 
      :class="{ no_select: settingStore.isSetting }"
    >
      <MainHeader />
      <MainClock v-if="!settingStore.isSetting" />
      <MainSearch v-if="!settingStore.isSetting" my-24 />
      <SiteContainer :key="settingStore.siteContainerKey" />
      <MainSetting />
      <TheFooter v-if="settingStore.getSettingValue('showFooter')" />
    </div>
    <Blank />
  </TheDoc>
</template>

<!-- 【关键修改5】保留这段路由配置，这是 vite-plugin-pages 识别子路由的关键 -->
<route lang="yaml">
path: /
children:
  - name: setting
    path: setting
    component: /src/components/Blank.vue
</route>
