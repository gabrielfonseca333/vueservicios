<template>
  <div>
    <h1>Empleados Oficios: {{oficio}}</h1>
    <div class="tarjeta">
        <table class="table table-dark">
            <thead>
                <tr>
                    <th>idEmpleado</th>
                    <th>apellido</th>
                    <th>salario</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="emp in empleados" :key="emp">
                    <td>{{emp.idEmpleado}}</td>
                    <td>{{emp.apellido}}</td>
                    <td>{{emp.salario}}</td>
                </tr>
            </tbody>
        </table>
    </div>
  </div>
</template>

<script>
import Global from '@/Global'
import axios from 'axios'

export default {
    name: "EmpleadosOficios",

    data(){
        return{
            oficio:"",
            empleados:[]
        }
    },

    methods: {
        loadEmpleados(){
            let oficio = this.$route.params.oficio
            this.oficio = oficio
            let request = "api/empleados/empleadosoficio/" + oficio
            let url = Global.urlApiEmpleados + request
            axios.get(url).then(response=>{
                this.empleados = response.data
            })
        }
    },
    mounted(){
        this.loadEmpleados();
    },

    watch:{
        '$route.params.oficio'(nextVal, oldVal){
            if(nextVal!=oldVal){
                this.loadEmpleados();
            }
        }
    }
}
</script>

<style>
@import "./../assets/css/styles"
</style>