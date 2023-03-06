<template>
  <div class="flex justify-center">
    <InputComponent v-model="text" />
    {{ text }}
  </div>
</template>

<script setup>
import InputComponent from './components/InputComponent.vue';
import { ref } from 'vue';

const text = ref("");
</script>
