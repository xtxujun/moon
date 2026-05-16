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
    <div p="8 sm:12 md:16" w="full" :class="{ 'no-select': settingStore.isSetting }" class="relative z-20">
      <MainHeader />

      <MainClock v-if="!settingStore.isSetting" />

      <!-- 内容卡片 - 提高层级 -->
      <div class="mt-6 max-w-[1420px] mx-auto relative z-30
                  bg-white/70 dark:bg-zinc-900/80 
                  backdrop-blur-2xl 
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
