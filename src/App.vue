<template>
  <div class="flex justify-center items-center h-screen">
    <InputComponent v-model="text" />
  </div>
</template>

<script setup>
import InputComponent from './components/InputComponent.vue';
import { ref } from 'vue';

const text = ref("");
</script>
