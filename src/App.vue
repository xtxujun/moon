<!-- 在 <template> 最外层添加 -->
<div class="bing-bg" :style="{ backgroundImage: `url(${currentBg})` }"></div>

<script setup>
import { ref, onMounted } from 'vue'

const currentBg = ref('')

// Bing 每日壁纸 API（推荐几个稳定免费的）
const fetchBingWallpaper = async () => {
  try {
    // 方法1（推荐，简单稳定）
    const res = await fetch('https://bing.biturl.top/?format=json')
    const data = await res.json()
    currentBg.value = data.url  // 高清原图

    // 方法2（备选）
    // const res = await fetch('https://www.bing.com/HPImageArchive.aspx?format=js&idx=0&n=1')
    // ...
  } catch (e) {
    // 降级默认背景
    currentBg.value = 'https://picsum.photos/1920/1080?random=1'
  }
}

onMounted(() => {
  fetchBingWallpaper()
  // 可选：每24小时刷新一次
  setInterval(fetchBingWallpaper, 86400000)
})
</script>

<style>
.bing-bg {
  position: fixed;
  top: 0; left: 0; right: 0; bottom: 0;
  background-size: cover;
  background-position: center;
  z-index: -1;
  transition: background-image 1.5s ease-in-out;
  filter: brightness(0.85); /* 可调亮度 */
}
</style>
