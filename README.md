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
