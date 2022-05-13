<script lang="ts">
import { defineComponent } from 'vue'
export default defineComponent({
  name: 'ResizeObserver'
})
</script>
<script setup lang="ts">
import { ref, computed, onMounted, onBeforeUnmount } from 'vue'
const w = ref(100)
const style = computed(() => {
  return {
    width: `${w.value}px`,
    height: '100px',
    background: '#6cf'
  }
})
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
</template>
