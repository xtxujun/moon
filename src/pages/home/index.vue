<script setup lang="ts">
import MainHeader from './components/MainHeader.vue'
import MainClock from './components/MainClock.vue'
import MainSearch from './components/MainSearch.vue'
import SiteContainer from './components/SiteContainer.vue'
import MainSetting from './components/MainSetting.vue'

defineOptions({
  name: 'HomePage',
})

const settingStore = useSettingStore()
</script>

<template>
  <TheDoc>
    <div p="12 sm:24" w="full sm:auto" :class="{ 'no-select': settingStore.isSetting }">
      <MainHeader />

      <MainClock v-if="!settingStore.isSetting" />

      <!-- 优化后的毛玻璃卡片区域 -->
      <div class="mt-8 max-w-[1100px] mx-auto 
                  bg-white/15 dark:bg-black/40 
                  backdrop-blur-3xl 
                  rounded-3xl border border-white/25 shadow-2xl 
                  p-8 sm:p-10">
        
        <MainSearch v-if="!settingStore.isSetting" class="mb-10" />

        <SiteContainer :key="settingStore.siteContainerKey" />
      </div>

      <MainSetting />

      <TheFooter v-if="settingStore.getSettingValue('showFooter')" />
    </div>
  </TheDoc>
</template>

<route lang="yaml">
path: /
children:
  - name: setting
    path: setting
    component: /src/components/Blank.vue
</route>
