<script setup lang="ts">
import { ref } from "vue";
let products = ref(["Хліб", "Молоко", "Сир", "Яблука"]);
defineProps({
  image: String,
  size: Number
});

</script>  
<template>
<div>
    <h2><slot>Вміст за замовчуванням</slot></h2>  
    <img :src="image" :width="size" :height="size">  
      <div v-for="(product, index) in products" :key="index">
        {{ index + 1 }}. {{ product }}    
        </div>    
        <slot name="info">ДЕФ</slot>
  </div>
</template>