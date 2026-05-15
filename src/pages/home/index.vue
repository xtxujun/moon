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
    <div p="8 sm:12 md:16" w="full" :class="{ 'no-select': settingStore.isSetting }">
      <MainHeader />

      <MainClock v-if="!settingStore.isSetting" />

      <!-- 优化版：更宽 + 更好的明亮/暗黑适配 -->
      <div class="mt-6 max-w-[1280px] mx-auto 
                  bg-white/70 dark:bg-black/50 
                  backdrop-blur-3xl 
                  rounded-3xl border border-white/30 dark:border-white/20 
                  shadow-2xl overflow-hidden">
        
        <div class="p-8 sm:p-10">
          <MainSearch v-if="!settingStore.isSetting" class="mb-10" />
          <SiteContainer :key="settingStore.siteContainerKey" />
        </div>
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
