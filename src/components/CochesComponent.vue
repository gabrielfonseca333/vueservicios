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
import ServiceCoches from "./../services/ServiceCoches"
const service = new ServiceCoches();

export default {
  name: "CochesComponent",
  data() {
    return {
      coches: [],
    };
  },
  mounted() {
    
    service.getCoches.then(result =>{
      this.coches = result
    })
    
  },
};
</script>

<style>
    @import "./../assets/css/styles";
</style>