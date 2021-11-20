<template>
  <div class="form-box">
    <label :for="name" class="form-label" :class="{required: !!required}">{{ libelle }}</label>
    <input class="form-control" :id="name" type="text" v-model="value" />
    <div class="form-message" v-show="meta.dirty">{{ errorMessage }}</div>
  </div>
</template>

<script setup lang="ts">
import {defineProps, defineEmits, watchEffect, toRefs} from 'vue'
import {useField} from 'vee-validate'

interface Props {
  name?: string;
  libelle: string;
  required?: boolean;
  modelValue?: string;
}

const props = defineProps<Props>()
const {modelValue} = toRefs(props)
const emit = defineEmits()

function isRequired(value: string) {
  if (value && value.trim()) {
    return true
  }
  return 'Field required'
}

const {errorMessage, value, meta} = useField('modelValue', isRequired)

if (modelValue && modelValue.value) {
  value.value = modelValue.value
}

watchEffect(() => emit('update:modelValue', value))
</script>
