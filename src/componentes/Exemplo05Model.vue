<script setup>
import { ref } from 'vue';

let texto = ref("");
</script>

<template>
    <input type="text" name="" id="" v-model="texto">
    <p>{{ texto }}</p>
</template>