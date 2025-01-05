<template>
  <button @click="notifyParent">Натисни мене</button>
</template>

<script setup>
import { defineEmits } from 'vue';

// Визначення подій, які можна емітити
const emit = defineEmits(['custom-event']);

// Функція, що емітить подію
function notifyParent() {
  emit('custom-event', 'Привіт, батьківський компонент!');
}
</script>