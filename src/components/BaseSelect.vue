<script setup>
  import { ref, watch } from 'vue'

  const props = defineProps({
    label: String,
    inputName: String,
    options:Array,
    multiple:{
      type:Boolean,
      default:false
    }
  })

  const listOpened = ref(false);
  const checkedValue = ref(props.multiple ? [] : "");
  const checkedLabel = ref("");
  const inputContainer = ref(null)

  function toggleList() {
    listOpened.value = !listOpened.value
  }
  function checkOption(option) {
    listOpened.value = false
    checkedLabel.value = option.label
    checkedValue.value = option.value
  }

  if(props.multiple) {
    watch(checkedValue,async () => {
        if(checkedValue.value.length) {
          checkedLabel.value = "Выбрано - " + checkedValue.value.length
        } else {
          checkedLabel.value = ""
        }
    })
  }

  document.addEventListener("click",(ev)=>{
    if(!inputContainer.value.contains(ev.target)) listOpened.value = false
  })
</script>

<template>
  <div class="input" :class="{list_opened:listOpened,has_value:checkedLabel}" ref="inputContainer">
    <div class="input__wrapper interactive" @click="toggleList">
      <span class="input__label">{{ label }}</span>
      <span class="input__value">{{ checkedLabel }}</span>
      <svg class="input__select-arrow" width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M5.22953 7.20999C5.37279 7.07216 5.56491 6.99685 5.76367 7.0006C5.96243 7.00435 6.15157 7.08686 6.28953 7.22999L9.99953 11.168L13.7095 7.22999C13.777 7.15565 13.8586 7.0956 13.9497 7.0534C14.0408 7.01119 14.1394 6.9877 14.2397 6.98431C14.34 6.98093 14.44 6.99771 14.5337 7.03366C14.6274 7.06962 14.713 7.12402 14.7853 7.19365C14.8576 7.26327 14.9152 7.3467 14.9546 7.43899C14.9941 7.53127 15.0146 7.63055 15.015 7.73092C15.0154 7.83129 14.9957 7.93072 14.9569 8.02332C14.9182 8.11592 14.8613 8.1998 14.7895 8.26999L10.5395 12.77C10.4696 12.8426 10.3857 12.9003 10.2929 12.9398C10.2001 12.9792 10.1003 12.9995 9.99953 12.9995C9.89871 12.9995 9.79893 12.9792 9.70615 12.9398C9.61337 12.9003 9.52949 12.8426 9.45953 12.77L5.20953 8.26999C5.0717 8.12674 4.99638 7.93462 5.00013 7.73585C5.00388 7.53709 5.08639 7.34795 5.22953 7.20999Z"/>
      </svg>
    </div>
    <div class="input__options-list">
      <template v-if="multiple">
        <label class="input__list-option interactive" v-for="option in options">
          <input type="checkbox"
                 v-model="checkedValue"
                 :value="option.value"
                 :name="inputName+'[]'"
                 class="input__list-option-radio" >
          <span class="input__list-option-label">{{ option.label }}</span>
        </label>
      </template>
      <template v-else>
        <label class="input__list-option interactive" @click="checkOption(option)" v-for="option in options">
          <input type="radio"
                 :value="option.value"
                 :name="inputName"
                 class="input__list-option-radio">
          <span class="input__list-option-label">{{ option.label }}</span>
        </label>
      </template>
    </div>
  </div>
</template>
