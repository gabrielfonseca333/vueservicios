<template>
  <div>
    <h1>Empleados</h1>
    <div class="tarjeta" style="margin-bottom:20px">
        <select v-model=id class="form-control" >
            <option v-for="emp in empleados" :key="emp" 
            :value="emp.idEmpleado">{{emp.apellido}}</option>
        </select>
        <button @click="mostrarDetalle()" class="btn btn-outline-dark">Mostrar Info</button>

        
    </div>

    <div v-if="empleadoSeleccionado.length != 0" class="tarjeta" style="border: 1px solid lightblue">
        <h2>{{empleadoSeleccionado.apellido}}</h2>
        <hr>
        <p><b>oficio: </b>{{empleadoSeleccionado.oficio}}</p>
        <p><b>salario: </b>{{empleadoSeleccionado.salario}}</p>
        
    </div>
  </div>
</template>

<script>
import Global from './..//Global'
import axios from 'axios'

export default {
    name: "EmpleadosDetalle",
    data(){
        return{
            empleados:[],
            id:0,
            empleadoSeleccionado:[]
        }
    },
    mounted(){
        let request = "api/empleados"
        let url = Global.urlApiEmpleados + request
        axios.get(url).then(response=>{
            this.empleados = response.data
        })

    },
    methods:{
        mostrarDetalle(){
            let request = "api/empleados/" + this.id
        let url = Global.urlApiEmpleados + request
        axios.get(url).then(response=>{
            this.empleadoSeleccionado = response.data
            console.log("🤖", this.empleadoSeleccionado)
        })
        }
    }
}
</script>

<style>
    @import "./../assets/css/styles";
</style>