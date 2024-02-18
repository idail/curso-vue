<script setup>
import { onMounted, ref } from 'vue';

let texto = ref("Hello World!");

onMounted(function(){
    setTimeout(function(){
        texto.value = "Alterando texto!";
    },3000);
});
</script>

<template>
    <h1>{{ texto }}</h1>
</template>