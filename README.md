# usefulComponents记录一些好用的轮子
## 1.vue3-count-to 滚动展示数字
``
npm install vue3-count-to
``
```
<CountTo
  :start-val="0"
  :end-val="102400"
  :duration="2600"
/>
```
[具体使用参考npm地址：https://www.npmjs.com/package/vue3-count-to](https://www.npmjs.com/package/vue3-count-to)
## 2.clipboard 复制到剪贴板
``
npm install clipboard --save
``
```
<template>
  <div>
    <el-input v-model="inputData" placeholder="Please input" style="width:400px; max-width:100%;" />
    <el-button type="primary" icon="el-icon-document" @click="handleClipboard(inputData, $event)">
      copy
    </el-button>
  </div>
</template>

<script setup lang='ts'>
import Clipboard from 'clipboard';
const inputData = ref('');

const handleClipboard = (text: string, event: MouseEvent) => {
  const clipboard = new Clipboard(event.target as Element, {
    text: () => text
  })
  clipboard.on('success', () => {
    ElMessage({
      message: 'Copy successfully',
      type: 'success',
      duration: 1500
    })
    clipboard.destroy()
  })
  clipboard.on('error', () => {
    ElMessage({
      message: 'Copy failed',
      type: 'error'
    })
    clipboard.destroy()
  });
  (clipboard as any).onClick(event)
}
</script>
```
[具体使用参考npm地址：https://www.npmjs.com/package/clipboard](https://www.npmjs.com/package/clipboard)
## 3.返回顶部
```
 <div class="main">
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="line">
      aaa
    </div>
    <div class="back" @click="backToTop">
      点我回顶部
    </div>
  </div>
```
```
const state = reactive({
  visible: false,
  isMoving: false,
  interval: 0
})
const easeInOutQuad = (t: number, b: number, c: number, d: number) => {
  if ((t /= d / 2) < 1) return (c / 2) * t * t + b
  return (-c / 2) * (--t * (t - 2) - 1) + b
}
const backToTop = () => {
  if (state.isMoving) return
  const start = window.pageYOffset
  let i = 0
  state.isMoving = true
  const interval = setInterval(() => {
    const next = Math.floor(easeInOutQuad(10 * i, start, -start, 500))
    if (next <= 0) {
      window.scrollTo(0, 0)
      clearInterval(interval)
      state.isMoving = false
    } else {
      window.scrollTo(0, next)
    }
    i++
  }, 16.7)
}
```
