<template>
  <!-- 
    关键点：
    1. relative: 建立定位上下文
    2. min-h-screen: 确保高度至少一屏
    3. flex/center: 让内容居中
    4. 绝对不要在这里写 bg-white 或 bg-[颜色]
  -->
  <main class="relative min-h-screen flex items-center justify-center p-4">
    <slot />
  </main>
</template>
