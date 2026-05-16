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

      <!-- 修复版：透明度降低 + 确保内容显示 -->
      <div class="mt-6 max-w-[1420px] mx-auto 
                  bg-white/65 dark:bg-zinc-900/80 
                  backdrop-blur-xl 
                  rounded-3xl border border-white/30 dark:border-white/20 
                  shadow-2xl overflow-hidden relative z-10">
        
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
