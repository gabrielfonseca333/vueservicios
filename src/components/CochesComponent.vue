<template>
  <div>
    <h1>Coches Component</h1>
    <div class="tarjeta">
      <table class="table table-hover">
        <thead>
          <tr class="table-dark">
            <th>MODELO</th>
            <th>IMAGEN</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="car in coches" :key="car">
            <td>{{ car.modelo }}</td>
            <td><img :src="car.imagen" /></td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Global from './../Global'
//SI NECESITAMOS VARIABLES DECLARADAS PARA UTILIZARLAS
//EN TODOS LOS METODOS (mounted, created, methods)
//LA DECLARAMOS AQUI


export default {
  name: "CochesComponent",
  data() {
    return {
      coches: [],
    };
  },
  mounted() {
    let request = "webresources/coches";
    //LAS VARIABLES DECLARADAS POR ENCIMA DE export default
    //NO UTILIZAN LA PALABRA this
    let url = Global.urlApiCoches + request;
    axios.get(url).then((response) => {
      console.log("⭐Leyendo...");
      this.coches = response.data;
    });
  },
};
</script>

<style>
    @import "./../assets/css/styles";
</style>