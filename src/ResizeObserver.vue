<script lang="ts">
import { defineComponent } from 'vue'
export default defineComponent({
  name: 'ResizeObserver'
})
</script>
<script setup lang="ts">
import { ref, computed, onMounted, onBeforeUnmount } from 'vue'
import MarkDownIt from 'markdown-it';

const w = ref(100)
const style = computed(() => {
  return {
    width: `${w.value}px`,
    height: '100px',
    background: '#6cf'
  }
})

const md = new MarkDownIt();
const html = ref('');
html.value = md.render('' +
' ```js ' +
`
const a = 10;
let b = '111'
` +
'```'
);
console.log(html)
const obs = new ResizeObserver(entries => {
  console.log(entries)
})
onMounted(() => {
  obs.observe(document.querySelector<HTMLElement>('.box')!)
})
onBeforeUnmount(() => {
  obs.disconnect()
})
</script>
<template>
  <h1>ResizeObserver</h1>
  <h5></h5>
  <div class="box" :style="style"></div>
  <div class="code" v-html="html"></div>
</template>
