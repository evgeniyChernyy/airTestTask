<script setup>
  import { ref } from 'vue'

  const opened = ref(false)

  document.addEventListener("ShowOverlay",()=>{
    opened.value = true
  })
  document.addEventListener("HideOverlay",()=>{
    opened.value = false
  })
</script>
<template>
  <div class="overlay" :class="{active:opened}"></div>
</template>
