<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { useSettingStore } from '@/stores/setting'

// 修改导入路径：去掉 "Main" 前缀，匹配实际文件名
import Header from '@/components/Header.vue'
import Clock from '@/components/Clock.vue'
import Search from '@/components/Search.vue'
import SiteContainer from '@/components/SiteContainer.vue'
import Setting from '@/components/Setting.vue'
import TheFooter from '@/components/TheFooter.vue'

const settingStore = useSettingStore()

// 保留原有的壁纸逻辑（如果之前加了的话）
const bingBg = ref('')
const fetchBingWallpaper = async () => {
  try {
    const res = await fetch('https://www.bing.com/HPImageArchive.aspx?format=js&idx=0&n=1')
    const data = await res.json()
    if (data.images && data.images.length > 0) {
      bingBg.value = 'https://www.bing.com' + data.images[0].url
    }
  } catch (error) {
    console.error(error)
  }
}

onMounted(() => {
  fetchBingWallpaper()
})
</script>
