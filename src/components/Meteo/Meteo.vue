<template>
  <div class="container">
    <h1 class="my-4 text-center">Application météo</h1>
    <div class="from-group my-5">
      <label for="position">Entrer le nom d'une ville</label>
      <input
        type="text"
        id="position"
        class="form-control"
        v-model="requete"
        v-on:keypress.enter="goMeteo"
      />
    </div>

    <div class="w-75 m-auto" v-if="temps">
      <h3 class="text-center mb-3">Position: {{ temps.name }}</h3>
      <div class="card text-center p-5">
        <p class="text-affichage">
          Température: {{ temps.main.temp.toFixed() }}°
        </p>
        <p class="text-affichage">Temps: {{ temps.weather[0].description }}</p>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "Meteo",
  data() {
    return {
      requete: "",
      temps: undefined,
      api_code: "0b9dc247855869891e7eb28a84e6a2f4",
      url_recherche: "https://api.openweathermap.org/data/2.5/weather?",
    };
  },
  methods: {
    goMeteo() {
      axios
        .get(
          `${this.url_recherche}q=${this.requete}&units=metric&APPID=${this.api_code}&lang=fr`
        )
        .then((reponse) => {
          this.temps = reponse.data;
        });
      this.requete = "";
    },
  },
};
</script>

<style scoped>
.text-affichage {
  font-size: 30px;
  font-weight: 300;
  line-height: 1.2;
}
</style>