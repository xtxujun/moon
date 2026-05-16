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

      <MainSearch v-if="!settingStore.isSetting" class="my-24" />

      <SiteContainer :key="settingStore.siteContainerKey" />

      <MainSetting />

      <TheFooter v-if="settingStore.getSettingValue('showFooter')" />
    </div>
  </TheDoc>
</template>
