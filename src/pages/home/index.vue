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

      <!-- 重点：给主要内容增加半透明毛玻璃卡片 -->
      <div class="mt-6 max-w-6xl mx-auto bg-white/10 dark:bg-black/30 backdrop-blur-2xl rounded-3xl border border-white/20 shadow-2xl p-8">
        <MainSearch v-if="!settingStore.isSetting" class="my-8" />

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
