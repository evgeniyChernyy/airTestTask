<script setup>
import TextInput from './TextInput.vue';
import BaseSelect from './BaseSelect.vue';
import { ref } from 'vue'

const opened = ref(false)
const placeTypeOptions = [{
  label:'Производственная площадь',
  value:'productionSquare'
},{
  label:'Складское помещение',
  value:'warehouse'
},{
  label:'Торговое место',
  value:'tradingSquare'
}]

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
        :name="'companyName'"
      />
      <TextInput
        :label="'Контактный телефон'"
        :name="'contactPhone'"
        :mask="'+7 (###) ###-##-##'"
      />
      <BaseSelect
        :label="'Тип помещения'"
        :inputName="'placeType'"
        :options="placeTypeOptions"
      />
    </div>
  </div>
</template>
