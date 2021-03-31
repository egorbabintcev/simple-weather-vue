<template>
  <div class="container">
    <city-input v-model="cityInput" @afterInput="fetchWeather"></city-input>
  </div>
</template>

<script>
import axios from "axios";
import CityInput from "@/components/CityInput";

const API_KEY = "a01b8bf4005d07aaea6f68a91dc2b7c3";
const API_URL = `https://api.openweathermap.org/data/2.5/weather`;

export default {
  name: "App",
  components: {
    CityInput,
  },
  data() {
    return {
      cityInput: "Moscow",
      weather: null,
    };
  },
  methods: {
    async fetchWeather() {
      try {
        const { data } = await axios.get(
          `${API_URL}?q=${this.cityInput}&appid=${API_KEY}&units=metric`
        );
        this.weather = data;
        console.log(data);
      } catch (err) {
        this.weather = null;
      }
    },
  },
  mounted() {
    this.fetchWeather();
  },
};
</script>

<style lang="scss">
@import "@/assets/sass/utils/functions";

#app {
  color: hsl(210, 29%, 24%);
  padding-top: rem(60);
}

.container {
  margin: 0 auto;
  max-width: 480px;
  padding: {
    left: rem(15);
    right: rem(15);
  }
}
</style>
