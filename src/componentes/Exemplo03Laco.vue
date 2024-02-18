<script setup>
let nomes = ["Idail", "Eliza", "Matheus", "Sthefany"];
</script>

<template>
    <ul>
        <li v-for="nome in nomes">{{ nome }}</li>
    </ul>
</template>