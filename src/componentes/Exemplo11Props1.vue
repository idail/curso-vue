<script setup>
import Exemplo11Props2 from './Exemplo11Props2.vue';
let cidade = "São Paulo";
let cidades = ["São Paulo","Rio de Janeiro","Curitiba","Florianópolis"];

function mensagem()
{
    alert("Função criada no compomente:Exemplo11Props1");
}
</script>

<template>
    <Exemplo11Props2 nome="Idail Neto" idade="32" :cidade="cidade" :cidades="cidades" :funcao="mensagem"></Exemplo11Props2>
</template>