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
    <div class="relative z-[10000] min-h-screen text-black p-12 sm:p-24 bg-white/30 backdrop-blur-xl rounded-3xl shadow-2xl overflow-hidden">

      <MainClock v-if="!settingStore.isSetting" />

      <MainSearch v-if="!settingStore.isSetting" class="my-24" />

      <SiteContainer :key="settingStore.siteContainerKey" />

      <MainSetting />

      <TheFooter v-if="settingStore.getSettingValue('showFooter')" />
    </div>
  </TheDoc>
</template>
