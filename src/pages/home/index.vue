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
    <div class="relative z-50 min-h-screen p-8 bg-white/90 dark:bg-black/90">
      <MainHeader />

      <MainClock v-if="!settingStore.isSetting" />

      <div class="max-w-[1400px] mx-auto mt-8 bg-white dark:bg-zinc-900 rounded-3xl shadow-2xl p-8">
        <MainSearch v-if="!settingStore.isSetting" class="mb-10" />
        <SiteContainer :key="settingStore.siteContainerKey" />
      </div>

      <MainSetting />

      <TheFooter v-if="settingStore.getSettingValue('showFooter')" />
    </div>
  </TheDoc>
</template>
