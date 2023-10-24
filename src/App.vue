<script>
import axios from "axios";
export default {
  data() {
    return {
      city: "",
      error: "",
      info: null,
      api: "85c828a0b2abcd5e9f26fd92b69e7aa1",
    };
  },
  computed: {
    cityName() {
      return this.city;
    },
  },
  methods: {
    getWeather() {
      if (this.city.trim().length < 2) {
        this.error = "Trebuie mai multe simboluri";
        return false;
      }

      this.error = "";
      axios
        .get(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=${this.api}`,
        )
        .then((res) => (this.info = res.data));
    },
  },
};
</script>

<template>
  <div class="wrapper">
    <h1>Meteo 2</h1>
    <p>
      Verifica temperatura in
      {{ city === "" ? "Orasul tau" : cityName }}
    </p>
    <input type="text" v-model="city" placeholder="Introduceti orasul" />
    <button v-if="city !== ''" @click="getWeather()">Verifica meteo</button>
    <button disabled v-else>Introdu orasul</button>
    <p class="error">{{ error }}</p>
    <p v-if="info !== null">{{ info }}</p>
  </div>
</template>

<style scoped>
.error {
  color: red;
}
.wrapper {
  width: 900px;
  height: 500px;
  border-radius: 50px;
  padding: 20px;
  text-align: center;
  color: white;
  background: #1f0f24;
}
.wrapper h1 {
  margin-top: 50px;
}

.wrapper p {
  margin-top: 20px;
}
.wrapper input {
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid #110813;
  color: white;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;
}
.wrapper input:focus {
  border-bottom-color: aqua;
}
.wrapper button {
  background: #e3bc4b;
  color: white;
  border-radius: 10px;
  border: 2px solid #b99935;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}
.wrapper button:hover {
  transform: scale(1.1) translateY(-5px);
}
</style>
