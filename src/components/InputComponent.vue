<template>
  <input v-model="localValue" class="bg-white border border-black h-fit rounded-md px-3 py-1" @keyup="onInput">
</template>

<script setup>
import { onMounted, ref } from 'vue'
import { watch } from "vue"

const props = defineProps({
  modelValue: {
    type: String,
    default: ''
  }
})

const emits = defineEmits(['update:modelValue'])

const incrAscii = function (v) {
  let code = v.charCodeAt(0)
  return String.fromCharCode(++code)
}

const modify = function (str) {
  return str.split('').map(x => incrAscii(x)).join('')
}

const localValue = ref('')

watch(() => props.modelValue, (value) => {
  localValue.value = value
})

watch(localValue, (value) => {
  emits('update:modelValue', value)
})

const onInput = function (e) {
  if (['Control', 'Alt', 'Shift', 'Meta', 'Backspace'].includes(e.key)) {
    return
  }
  emits('update:modelValue', localValue.value.slice(0, -1) + modify(e.key))
}

onMounted(() => {
  localValue.value = modify(props.modelValue)
})
</script>
