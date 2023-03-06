<template>
  <input
    type="text"
    class="rounded-md border-1 bg-stone-500 border-slate-400 m-1 px-2 py-1"
  >
  <input type="text" v-model="second" class="bg-red-600 p-2">
  {{ second }}
</template>

<script setup>
import { ref , watch } from 'vue';

const second = ref("")
//const text = ref(props.modelValue);

const props = defineProps ({
  modelValue: {
    type: String,
    default:''
  }
})
const emits = defineEmits(["update:modelValue"]);

console.log(props.modelValue);

watch(
  () => props.modelValue,
  (value) => {
    
    emits("update:modelValue", "changed");
  }
  
);

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


/*
  () => props.modelValue,
  (value) => { 
    const letters = [...text];
    console.log(letters)
    //emits("update:modelValue", incrementedText);
    emits("update:modelValue", value+"added");
  }
*/

//String.fromCharCode('A'.charCodeAt() + 1) // Returns B
</script>


