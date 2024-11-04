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
import ServiceEmpleados from "./../services/ServiceEmpleados"
const service = new ServiceEmpleados();

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
        service.getEmpleados().then(result=>{
            this.empleados = result;
        })

    },
    methods:{
        mostrarDetalle(){
            service.findEmpleados(this.id).then(result=>{
                this.empleadoSeleccionado = result
            })
        }
    }
}
</script>

<style>
    @import "./../assets/css/styles";
</style>