<template>
  <div class="container">
    <form v-if="!isSubmitted">
      <div class="row">
        <div
          class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3"
        >
          <h1>Ingresa tu información</h1>
          <hr />
          <div class="form-group">
            <label for="semilla">Semilla</label>
            <input
              type="text"
              id="semilla"
              class="form-control"
              placeholder="Aguacate"
              :value="userData.semilla"
              @input="userData.semilla = $event.target.value"
            />
          </div>
          <div class="form-group">
            <label for="cantidad">Cantidad</label>
            <input
              type="number"
              id="cantidad"
              class="form-control"
              v-model="userData.cantidad"
              min="1"
            />
          </div>
          <div class="form-group">
            <label for="longitud">Longitud</label>
            <input
              type="number"
              id="longitud"
              class="form-control"
              v-model="userData.latitud"
            />
          </div>
          <div class="form-group">
            <label for="latitud">Latitud</label>
            <input
              type="number"
              id="latitud"
              class="form-control"
              v-model="userData.longitud"
            />
          </div>
        </div>
      </div>
      <div class="row">
        <div
          class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3"
        ></div>
      </div>
      <hr />
      <div class="row">
        <div
          class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3"
        >
          <button class="btn btn-primary" @click.prevent="submitted">
            Enviar!
          </button>
        </div>
      </div>
    </form>
    <hr />
    <div class="row" v-if="isSubmitted">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
        <div class="panel panel-default">
          <div class="panel-heading">
            <h4>Información suministrada</h4>
          </div>
          <div class="panel-body">
            <p>Semilla: {{ userData.semilla }}</p>
            <p>Cantidad: {{ userData.cantidad }}</p>
            <p>Latitud: {{ userData.latitud }}</p>
            <p>Longitud: {{ userData.longitud }}</p>
          </div>
        </div>
      </div>
      <button @click="reloadPage" class="btn btn-primary">Nueva consulta</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      userData: {
        semilla: "",
        cantidad: 0,
        latitud: 0,
        longitud: 0,
      },
      isSubmitted: false,
      slides: [
        "https://cdn.pixabay.com/photo/2016/11/30/15/00/apples-1872997_960_720.jpg",
        "https://cdn.pixabay.com/photo/2016/08/03/01/09/carrot-1565597_960_720.jpg",
        "https://cdn.pixabay.com/photo/2018/06/29/22/45/wheat-3506758_960_720.jpg",
        "https://cdn.pixabay.com/photo/2016/08/01/17/08/tomatoes-1561565_960_720.jpg",
        "https://cdn.pixabay.com/photo/2014/07/06/17/20/tractor-385681_960_720.jpg",
        "https://cdn.pixabay.com/photo/2015/10/05/14/50/farm-972717_960_720.jpg",
        "https://cdn.pixabay.com/photo/2016/01/02/01/59/oranges-1117628_960_720.jpg",
        "https://cdn.pixabay.com/photo/2018/09/26/21/24/corn-3705687_960_720.jpg"
      ]
    };
  },
  methods: {
    submitted() {
      this.isSubmitted = true;
      axios.post('https://back-evergreen-pro.herokuapp.com/api/siembra', this.userData)
        .then(res => console.log(res))
        .catch(error => console.log(error));
    },
    reloadPage() {
      location.reload();
    }
  }
};
</script>

<style></style>
