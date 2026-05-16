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

      <!-- Bing 磨砂白透效果核心修改区域 -->
      <div class="mt-6 max-w-[1380px] mx-auto relative z-10
                  bg-white/70 dark:bg-black/60 
                  backdrop-blur-2xl 
                  rounded-3xl border border-white/30 dark:border-white/10 
                  shadow-2xl overflow-hidden">
        
        <div class="p-8 sm:p-10">
          <MainSearch v-if="!settingStore.isSetting" class="my-8" />
          <SiteContainer :key="settingStore.siteContainerKey" />
        </div>
      </div>

      <MainSetting />

      <TheFooter v-if="settingStore.getSettingValue('showFooter')" />
    </div>
  </TheDoc>
</template>
