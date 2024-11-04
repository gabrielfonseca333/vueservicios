<template>
  <div>
    <h1>Home</h1>
    <div class="tarjeta">
      <h2>{{mensaje}}</h2>
    </div>
    
  </div>
</template>

<script>
import ServiceEjemplo from "./../services/ServiceEjemplo"
//PARA PODER UTILIZAR EL SERVICIO, NECESITAMOS UNA CONSTANTE INSTANCIADA 
//CON LA CLASE DEL SERVICIO NECESARIO
const service = new ServiceEjemplo();

export default {
    name: "HomeComponent",
    data(){
      return{
        mensaje: ""
      }
    },
    mounted(){
      this.mensaje = service.getSaludo("Gabriel")
    }
}
</script>

<style>
@import "./../assets/css/styles";
</style>