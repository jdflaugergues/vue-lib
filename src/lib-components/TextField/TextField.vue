<template>
  <div class="form-box">
    <label :for="name" class="form-label" :class="{required: !!required}">{{ libelle }}</label>
    <input class="form-control" :id="name" type="text" v-model="value">
    <div class="form-message" v-show="true">{{ errorMessage }}</div>
  </div>
</template>

<script lang="ts">
import { defineComponent, watchEffect, toRefs } from 'vue'
import { useField } from 'vee-validate'

export default defineComponent({
  name: 'pop-text',
  props: {
    name: String,
    libelle: String,
    required: Boolean,
    modelValue: String
  },
  setup(props, {emit}) {
    const {modelValue, name, required, libelle} = toRefs(props)

    function isRequired(value: string) {
      if (value && value.trim()) {
        return true
      }
      return 'Field required'
    }

    const {errorMessage, value} = useField('modelValue', isRequired)

    if (modelValue && modelValue.value) {
      value.value = modelValue.value
    }

    watchEffect(() => {
      console.log('value watchEffect', value.value)
      emit('update:modelValue', value.value)
    })

    return {errorMessage, value, name, required, libelle}
  }
})
</script>
