<script setup>
  import { ref } from "vue"
  import { vMaska } from "maska/vue"

  const props = defineProps({
    label: String,
    inputName: String,
    type: {
      type:String,
      required:true
    },
  })

  const masks = ref({
    number:{
      number: {
        locale: "ru",
        fraction: 2,
        unsigned: true
      }
    },
    date:{
      mask:'##.##.####',
      tokens:''
    }
  })

  function postProcessInput(event){
      if(props.type === 'date' && event instanceof InputEvent && event.target.value !== ""){
        let parts = event.target.value.split(".")

        if(parts[0] > 31) parts[0] = 31
        if(parts[1] && parts[1] > 12) parts[1] = 12

        event.target.value = parts.join(".")
      }
  }
</script>

<template>
  <div class="range">
    <span class="range__label">{{ label }}</span>
    <div class="range__inputs-container">
      <div class="range__input-container">
        <label class="range__input-label">
          <span class="range__input-label-text">{{ type === 'number' ? 'от' : 'с' }}</span>
          <input type="text" class="range__input-field" :name="inputName + 'From'"
                 v-maska="masks[type]"
                 @input="postProcessInput"
          >
        </label>
      </div>
      <div class="range__input-container">
        <label class="range__input-label">
          <span class="range__input-label-text">{{ type === 'number' ? 'до' : 'по' }}</span>
          <input type="text" class="range__input-field" :name="inputName + 'To'"
                 v-maska="masks[type]"
                 @input="postProcessInput"
          >
        </label>
      </div>
    </div>
  </div>
</template>
