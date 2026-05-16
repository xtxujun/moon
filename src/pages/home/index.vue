<script setup lang="ts">
import { ref, onMounted } from 'vue'
import MainHeader from './components/MainHeader.vue'
import MainClock from './components/MainClock.vue'
import MainSearch from './components/MainSearch.vue'
import SiteContainer from './components/SiteContainer.vue'
import MainSetting from './components/MainSetting.vue'
import TheFooter from './components/TheFooter.vue' // 确保路径正确

// 1. 定义壁纸变量
const bingBg = ref('')

// 2. 获取必应壁纸的逻辑
const fetchBingWallpaper = async () => {
  try {
    // 请求必应接口
    const res = await fetch('https://www.bing.com/HPImageArchive.aspx?format=js&idx=0&n=1')
    const data = await res.json()
    if (data.images && data.images.length > 0) {
      // 拼接完整的图片链接
      bingBg.value = 'https://www.bing.com' + data.images[0].url
    }
  } catch (error) {
    console.error('获取壁纸失败:', error)
  }
}

// 页面加载时执行
onMounted(() => {
  fetchBingWallpaper()
})

const settingStore = useSettingStore()
</script>

<template>
  <!-- 3. 背景图层：固定在屏幕最底层 -->
  <div 
    class="fixed inset-0 w-full h-full bg-cover bg-center bg-no-repeat z-[-1] transition-opacity duration-1000"
    :style="{ backgroundImage: 'url(' + bingBg + ')' }"
  ></div>

  <!-- 4. 内容层：必须把背景色去掉，或者改为半透明 -->
  <TheDoc>
    <div p="12 sm:24" w="full sm:auto" bg="transparent" :class="{ no_select: settingStore.isSetting }">
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

<route lang="yaml">
path: /
children:
  - name: setting
    path: setting
    component: /src/components/Blank.vue
</route>
