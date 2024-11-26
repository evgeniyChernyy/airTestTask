<script setup>
import TextInput from './TextInput.vue';
import BaseSelect from './BaseSelect.vue';
import BaseRange from './BaseRange.vue';
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

  function submitResidentRequestForm(){
    fetch("api/V1/resident.php",{
      method: 'POST',
      body: new FormData(document.forms.residentRequestForm)
    })
    .then((response)=>{
      if(response.ok) return response.json()
      else throw new Error("Что-то пошло не так")
    })
    .then((result) => alert(result.text))
    .catch((error) => alert(error))
  }
</script>

<template>
  <div class="popup" :class="{active:opened}">
    <form id="residentRequestForm">
      <div class="popup__header">
        <p class="popup__title">Заполните заявку, чтобы стать резидентом</p>
      </div>
      <div class="popup__content">
        <TextInput
          :label="'Наименование организации / ИП'"
          :inputName="'companyName'"
        />
        <TextInput
          :label="'Контактный телефон'"
          :inputName="'contactPhone'"
          :mask="'+7 (###) ###-##-##'"
        />
        <BaseSelect
          :label="'Тип помещения'"
          :inputName="'placeType'"
          :options="placeTypeOptions"
        />
        <TextInput
          :label="'Адрес'"
          :inputName="'address'"
        />
        <BaseRange
          :label="'Площадь помещения (м²)'"
          :inputName="'square'"
          :type="'number'"
        />
        <BaseRange
          :label="'Дата начала аренды'"
          :inputName="'rentDate'"
          :type="'date'"
        />
      </div>
      <div class="popup__footer">
        <button class="btn" @click="submitResidentRequestForm" type="button">Отправить</button>
      </div>
    </form>
  </div>
</template>
