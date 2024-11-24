<script setup>
  import { ref } from 'vue'

  defineProps({
    label: String,
  })

  const text = ref("")
  const focused = ref(false)

  function focusHandler(){
    focused.value = true
  }
  function blurHandler(){
    focused.value = false
  }
</script>

<template>
  <div class="input" :class="{has_value:focused || text.length}">
    <label class="input__wrapper">
      <span class="input__label">{{ label }}</span>
      <input
            class="input__input-field"
            type="text"
             v-model="text"
             @focus="focusHandler"
             @blur="blurHandler"
      >
    </label>
  </div>
</template>
