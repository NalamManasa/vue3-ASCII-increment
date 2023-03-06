<template>
  <input
    type="text"
    v-model="localValue"
    class="rounded-md outline-slate-600 bg-slate-200 m-1 px-2 py-1"
  >

</template>

<script setup>
import { ref , watch } from 'vue';

const props = defineProps ({
  modelValue: {
    type: String,
    default:'',
  }
})

const emits = defineEmits(["update:modelValue"]);
const localValue = ref(props.modelValue);
const length = ref(0);
let count = 0;

const jump_ascii = function(value){
  if(count === 1){
    const string = value;
    let newString = '';
    for (let index = 0; index < string.length; index++) {
      newString = newString + String.fromCharCode(string.charCodeAt(index) + 1);
    }
    return newString;
  }
}

const saveLength = function(len){
  length.value = len;
}

watch(
  () => props.modelValue,
  (value) => {
    if(length.value !== value.length ){
      count = 1;
      localValue.value = jump_ascii(value);
      saveLength(value.length);
    }
  }
);

watch(localValue, (value) => {
  emits("update:modelValue", value);
}
)
</script>
