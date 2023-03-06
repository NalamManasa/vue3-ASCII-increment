<template>
  <div class="flex justify-center">
    <InputComponent v-model="text" />
  </div>
</template>

<script setup>
import InputComponent from './components/InputComponent.vue';
import { ref } from 'vue';

const text = ref("asdfgh");

console.log(text.value);

</script>
