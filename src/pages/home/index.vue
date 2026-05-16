<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { useSettingStore } from '@/stores/setting' // 确保路径正确

// 【关键修改】请根据你 src/components/ 下实际的文件名修改下面的路径
// 如果文件名是 Header.vue，就写 './Header.vue' 或者 '@/components/Header.vue'
import MainHeader from '@/components/Header.vue'
import MainClock from '@/components/Clock.vue'
import MainSearch from '@/components/Search.vue'
import SiteContainer from '@/components/SiteContainer.vue'
import MainSetting from '@/components/Setting.vue'
import TheFooter from '@/components/TheFooter.vue' // 确认是否有这个文件，没有则删除引用

defineOptions({
  name: 'HomePage',
})

const settingStore = useSettingStore()
</script>

<template>
  <TheDoc>
    <!-- 这里的类名保持不变，确保背景透明 -->
    <div class="relative z-[10000] min-h-screen p-12 sm:p-24 bg-transparent">
      <MainHeader />

      <MainClock v-if="!settingStore.isSetting" />

      <MainSearch v-if="!settingStore.isSetting" class="my-24" />

      <SiteContainer :key="settingStore.siteContainerKey" />

      <MainSetting v-if="settingStore.isSetting" />

      <TheFooter />
    </div>
  </TheDoc>
</template>

<style scoped>
/* 确保没有局部样式覆盖背景 */
</style>
