<script setup>
import TextInput from './TextInput.vue';
import { ref } from 'vue'

const opened = ref(false)

document.addEventListener("OpenResidentRequestPopup",()=>{
  opened.value = true
})
</script>

<template>
  <div class="popup" :class="{active:opened}">
    <div class="popup__header">
      <p class="popup__title">Заполните заявку, чтобы стать резидентом</p>
    </div>
    <div class="popup__content">
      <TextInput
        :label="'Наименование организации / ИП'"
      />
    </div>
  </div>
</template>
