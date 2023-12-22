<script>
import axios from 'axios'
export default {
    name: 'clientes',
    data() {
        return {
            clientes: [],
            cliente: {},
            titulo: 'Listagem de Clientes'
        }
    },
    methods: {
        loadClientes() {
            axios.defaults.headers.common['Access-Control-Allow-Origin'] = '*'
                axios.get('http://localhost:4000/clientes')
                .then(resultado => {
                    console.log(resultado)
                    this.clientes = resultado.data
                })
                .catch(e => console.log(e.message))
                
        },
        mandaCliente() {
            this.cliente.filhos=[]
            axios.defaults.headers.common['Access-Control-Allow-Origin'] = '*'
            axios.post('http://localhost:4000/clientes', this.cliente)
            .then (resultado => {
                this.clientes = resultado.data
                this.cliente = {}
            })
            .catch(e => console.log(e))
        }
    }
}

</script>

<template>
<h1> {{ titulo }} </h1>
<button id="btn" type="button" @click="loadClientes">Carregar Clientes</button>
<table class="tabela" cellpadding="0" cellspacing="0" width="100%">
    <tr>
        <td class="col bg">Nome</td>
        <td class="col bg">Idade</td>
        <td class="col bg">Tem Filhos?</td>
    </tr>
    <tr v-for="cliente in this.clientes" :key="cliente.nome">
        <td class="col" align="left">{{ cliente.nome }}</td>
        <td class="col" align="center">{{ cliente.idade }}</td>
        <td class="col" align="left">{{ cliente.filhos.length > 0 ? `SIM tem ${cliente.filhos.length} filhos` : 'NÃO' }}</td>  
    </tr>    
</table>
<input type="text" v-model="cliente.nome" />
<input type="text" v-model="cliente.idade" />

<button class="btn2" type="button" @click="mandaCliente">Carregar Clientes</button>
</template>

<style>
#btn {
    color: white;
    background-color: green;
    margin-bottom: 15px;
}
.btn2 {
    color: white;
    background-color: red;
    margin-top: 15px;
}
.tabela {
    border: 1px solid grey;
}
.col {
    border: 1px solid grey;
    padding:4px;
}
.bg {
    background-color: brown;
    color: white;
}
</style>