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
    <div p="8 sm:12 md:16" w="full" class="relative z-50">
      <MainHeader />

      <MainClock v-if="!settingStore.isSetting" />

      <!-- 测试版：极简 + 高层级 + 低透明度 -->
      <div class="mt-6 max-w-[1420px] mx-auto relative z-50
                  bg-white/85 dark:bg-zinc-900/90 
                  backdrop-blur-xl 
                  rounded-3xl border border-white/50 shadow-2xl">
        
        <div class="p-8 sm:p-12">
          <MainSearch v-if="!settingStore.isSetting" class="mb-10" />
          <SiteContainer :key="settingStore.siteContainerKey" />
        </div>
      </div>

      <MainSetting />

      <TheFooter v-if="settingStore.getSettingValue('showFooter')" />
    </div>
  </TheDoc>
</template>
