<template>
  <input
    type="text"
    class="rounded-md border-1 bg-stone-500 border-slate-400 m-1 px-2 py-1"
  >
  <input type="text" v-model="localValue" class="bg-red-600 rounded-md p-2">

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

/*
const string = props.modelValue;


for (let index = 0; index < string.length; index++) {
  //newString =newString + String.fromCharCode(string.charCodeAt(index) + 1);
}


watch(
  second,
  (value) => {
    console.log("here")
    const string = value;
    let newString = '';
    for (let index = 0; index < string.length; index++) {
      newString = newString + String.fromCharCode(string.charCodeAt(index) + 1);
    }
    console.log( newString )
    second.value = newString
    
  }
)



  () => props.modelValue,
  (value) => { 
    const letters = [...text];
    console.log(letters)
    //emits("update:modelValue", incrementedText);
    emits("update:modelValue", value+"added");
  }
*/

</script>
