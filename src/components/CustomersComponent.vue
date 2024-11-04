<template>
  <div>
    <h1>Customers</h1>
    <div class="tarjeta" style="margin-bottom: 20px">
        <input v-model="id" type="text" placeholder="Introduce el ID" class="form-control">
        <button @click="buscarCliente()" class="btn btn-outline-dark">Buscar 🔍</button>
    </div>

    <div class="tarjeta" style="margin-bottom: 20px; border: 1px solid lightblue"
    
    v-for="cli in customerBuscado" :key="cli">
        <!-- aqui mostrar los detalles -->
        <h2>{{cli.contactName}}</h2>
        <hr>
        <div style="text-align: left;">
            <p><b>Compañía:</b> {{cli.companyName}}</p>
        <p style="background-color: yellow"><b>Pais:</b> {{cli.country}}</p>
        <p><b>Ciudad:</b> {{cli.city}}</p>
        <p><b>Direccion:</b> {{cli.address}}</p>
        <p class="rubik-wet-paint-regular"><b>Teléfono:</b> {{cli.phone}}</p>
        </div>
        
    </div>

    <div class="tarjeta">
        <table class="table table-hover">
        <thead>
            <tr class="table-dark">
                <th>ID</th>
                <th>Nombre</th>
                <th>Compañía</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="cliente in customers" :key="cliente">
                <td>{{cliente.id}}</td>
                <td>{{cliente.contactName}}</td>
                <td>{{cliente.companyName}}</td>
            </tr>
        </tbody>
    </table>
    </div>
    
  </div>
</template>

<script>
import axios from 'axios'
import Global from './../Global'

export default {
    name:"CustomersComponent",
    data(){
        return{
            customers:[],
            customerBuscado:[],
            id:""
        }
    },
    mounted(){
        let request = "customers"
        let url = Global.urlApiCustomers + request
        axios.get(url).then(response=>{
            this.customers = response.data.results
        })
    },
    methods:{
        buscarCliente(){
            let request = "customers/" + this.id
        let url = Global.urlApiCustomers + request
        axios.get(url).then(response=>{
            this.customerBuscado = response.data
            console.log("🔷🆒🍪", this.customerBuscado)
        })
        }
    }
}
</script>

<style>
    @import "./../assets/css/styles";
</style>