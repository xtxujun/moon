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
    <div class="relative z-30 min-h-screen p-6 sm:p-8 md:p-12">
      <MainHeader />

      <MainClock v-if="!settingStore.isSetting" />

      <!-- 内容主卡片 -->
      <div class="max-w-[1420px] mx-auto mt-6 
                  bg-white/85 dark:bg-zinc-900/90 
                  backdrop-blur-2xl rounded-3xl border border-white/40 
                  shadow-2xl overflow-hidden relative z-40">
        
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
