<script setup>
    function validaFormulario(event)
    {
        alert("Formulário enviado");
        event.preventDefault();
    }
</script>

<template>
    <form action="https://idailneto.com.br" @submit="validaFormulario">
        <input type="submit" value="Enviar formulário">
    </form>
</template>