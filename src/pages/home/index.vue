<script setup lang="ts">
import { ref, onMounted } from 'vue'
// 【关键修改1】路径必须用 @/ 开头，指向 src/components，不能用 ./components
import MainHeader from '@/components/MainHeader.vue'
import MainClock from '@/components/MainClock.vue'
import MainSearch from '@/components/MainSearch.vue'
import SiteContainer from '@/components/SiteContainer.vue'
import MainSetting from '@/components/MainSetting.vue'
import TheFooter from '@/components/TheFooter.vue'

defineOptions({
  name: 'HomePage',
})

const settingStore = useSettingStore()
</script>

<template>
  <TheDoc>
    <div class="relative z-[10000] min-h-screen p-12 sm:p-24 bg-white/90 dark:bg-zinc-900/90">
      <MainHeader />

      <MainClock v-if="!settingStore.isSetting" />

      <MainSearch v-if="!settingStore.isSetting" class="my-24" />

      <SiteContainer :key="settingStore.siteContainerKey" />

      <MainSetting />

      <TheFooter v-if="settingStore.getSettingValue('showFooter')" />
    </div>
  </TheDoc>
</template>

