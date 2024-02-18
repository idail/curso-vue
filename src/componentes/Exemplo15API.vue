<script setup>
import 'bootstrap/dist/css/bootstrap.min.css';
import { onMounted, ref } from 'vue';

let produtos = ref([]);

let btnCadastrar = ref(true);

onMounted(function () {
    fetch("http://localhost:3000/produtos")
        .then(requisicao => requisicao.json())
        .then(retorno => produtos.value = retorno);
});

let obj = ref({ "id": 0, "produto": "", "valor": 0 });

function cadastrar(event) {
    fetch("http://localhost:3000/produtos", {
        method: "POST",
        body: JSON.stringify(obj.value),
        headers: { "Content-Type": "application/json" }
    }).then(requisicao => requisicao.json()).then(retorno => {
        produtos.value.push(retorno)

        obj.value.produto = "";
        obj.value.valor = 0;
    })

    event.preventDefault();
}

function selecionar(indice) {
    obj.value = {
        id: produtos.value[indice].id,
        produto: produtos.value[indice].produto,
        valor: produtos.value[indice].valor
    }

    btnCadastrar.value = false;
}

function editar() {
    fetch("http://localhost:3000/produtos/" + obj.value.id, {
        method: "put",
        body: JSON.stringify(obj.value),
        headers: { "Content-Type": "application/json" }
    }).then(requisicao => requisicao.json()).then(retorno => {

        let indiceProduto = produtos.value.findIndex(objP => {
            return objP.id === retorno.id;
        });

        produtos.value[indiceProduto] = retorno;

        btnCadastrar.value = true;

        obj.value.id = 0;
        obj.value.produto = "";
        obj.value.valor = 0;
    })
}

function remover() {
    fetch("http://localhost:3000/produtos/" + obj.value.id, {
        method: "delete",
        headers: { "Content-Type": "application/json" }
    }).then(requisicao => requisicao.json()).then(function () {

        let indiceProduto = produtos.value.findIndex(objP => {
            return objP.id === obj.value.id;
        });

        produtos.value.splice(indiceProduto,1);

        btnCadastrar.value = true;

        obj.value.id = 0;
        obj.value.produto = "";
        obj.value.valor = 0;
    })
}
</script>

<style>
form {
    width: 50%;
    margin: 30px auto;
    text-align: center;
}

input {
    margin-bottom: 10px;
}

.espacamentoBtn {
    margin-left: 5px;
    margin-right: 5px;
}
</style>

<template>
    <form @submit="cadastrar">
        <input type="hidden" name="" id="" v-model="obj.id">
        <input type="text" class="form-control" name="" id="" placeholder="Produto" v-model="obj.produto">
        <input type="number" class="form-control" name="" id="" placeholder="Valor" v-model="obj.valor">
        <input type="submit" v-if="btnCadastrar" class="btn btn-primary" name="" id="" value="Cadastrar">
        <input type="button" v-if="!btnCadastrar" @click="editar" value="Editar" class="btn btn-primary espacamentoBtn">
        <input type="button" v-if="!btnCadastrar" @click="remover" value="Remover" class="btn btn-primary">
    </form>

    <table class="table table-striped">
        <thead>
            <tr>
                <th>Produto</th>
                <th>Valor</th>
                <th>Selecionar</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(p, indice) in produtos">
                <td>{{ p.produto }}</td>
                <td>{{ p.valor }}</td>
                <td><button @click="selecionar(indice)" class="btn btn-primary">Selecionar</button></td>
            </tr>
        </tbody>
    </table>
</template>