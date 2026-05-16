<script setup lang="ts">
import MainHeader from '@/components/MainHeader.vue'
import MainClock from '@/components/MainClock.vue'
import MainSearch from '@/components/MainSearch.vue'
import SiteContainer from '@/components/SiteContainer.vue'
import MainSetting from '@/components/MainSetting.vue'
import TheFooter from '@/components/TheFooter.vue' // 确保路径正确

defineOptions({
  name: 'HomePage',
})

const settingStore = useSettingStore()
</script>

<template>
  <TheDoc>
    <!-- 修改了这一行：删除了 bg-white/90 和 dark:bg-zinc-900/90 -->
    <div class="relative z-[10000] min-h-screen p-12 sm:p-24 bg-transparent">
      <MainHeader />

      <MainClock v-if="!settingStore.isSetting" />

      <MainSearch v-if="!settingStore.isSetting" class="my-24" />

      <SiteContainer :key="settingStore.siteContainerKey" />

      <MainSetting />

      <TheFooter v-if="settingStore.getSettingValue('showFooter')" />
    </div>
  </TheDoc>
</template>

<!-- 保留这段路由配置，它负责生成 /setting 页面 -->
<route lang="yaml">
path: /
children:
  - name: setting
    path: setting
    component: /src/components/Blank.vue
</route>
