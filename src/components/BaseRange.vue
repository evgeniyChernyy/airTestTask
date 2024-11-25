<script setup>
  import { ref } from "vue"
  import { vMaska } from "maska/vue"

  defineProps({
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
          >
        </label>
      </div>
      <div class="range__input-container">
        <label class="range__input-label">
          <span class="range__input-label-text">{{ type === 'number' ? 'до' : 'по' }}</span>
          <input type="text" class="range__input-field" :name="inputName + 'To'"
                 v-maska="masks[type]"
          >
        </label>
      </div>
    </div>
  </div>
</template>
