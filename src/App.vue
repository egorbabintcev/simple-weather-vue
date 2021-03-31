<template>
  <div class="container">
    <div class="bg" :class="weather?.main.temp > 20 ? 'warm' : ''"></div>
    <city-input v-model="cityInput" @afterInput="fetchWeather"></city-input>
    <weather-display v-if="weather" :weather="weather"></weather-display>
    <weather-fallback v-else></weather-fallback>
  </div>
</template>

<script>
import axios from "axios";
import CityInput from "@/components/CityInput";
import WeatherDisplay from "@/components/WeatherDisplay";
import WeatherFallback from "@/components/WeatherFallback";

const API_KEY = process.env.VUE_APP_API_TOKEN;
console.log(process.env);
const API_URL = `https://api.openweathermap.org/data/2.5/weather`;

export default {
  name: "App",
  components: {
    CityInput,
    WeatherDisplay,
    WeatherFallback,
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
}

.container {
  margin: 0 auto;
  max-width: 480px;
  min-height: 100vh;
  position: relative;
  padding: {
    left: rem(15);
    right: rem(15);
    top: rem(60);
  }
}

.bg {
  background: {
    image: url("./assets/img/cold-bg.jpg");
    position: center;
    repeat: no-repeat;
    size: cover;
  }
  bottom: 0;
  left: 0;
  position: absolute;
  right: 0;
  top: 0;
  transition: 0.4s;
  z-index: -1;

  &.warm {
    background-image: url("./assets/img/warm-bg.jpg");
  }
}
</style>
