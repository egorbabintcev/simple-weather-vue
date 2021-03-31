<template>
  <div class="weather-display">
    <p class="weather-display__name">
      {{ weather.name }}, {{ weather.sys.country }}
    </p>
    <h2 class="weather-display__temp">{{ temp }}°</h2>
  </div>
</template>

<script>
export default {
  name: "WeatherDisplay",
  props: ["weather"],
  computed: {
    temp() {
      return Math.round(this.weather?.main.temp);
    },
    daytime() {
      const time = new Date().getHours();
      if (time > 5 && time < 12) return "morning";
      if (time > 12 && time < 17) return "day";
      if (time > 17 && time < 12) return "evening";
      else return "night";
    },
  },
};
</script>

<style lang="scss">
@import "@/assets/sass/utils/functions";
@import "@/assets/sass/utils/mixins";

.weather-display {
  align-items: center;
  display: flex;
  flex-direction: column;

  &__name {
    letter-spacing: 0.03em;
    font: {
      size: rem(32);
      weight: 700;
    }

    &:last-of-type {
      margin-bottom: rem(30);
    }
  }

  &__temp {
    position: relative;
    font: {
      size: rem(128);
      weight: 900;
    }

    &::before {
      background-color: hsla(0, 0%, 100%, 0.5);
      border-radius: rem(16);
      box-shadow: rem(3) rem(3) rem(8) 0 hsla(0, 0%, 10%, 0.25);
      height: 120%;
      left: 50%;
      top: 50%;
      transform: translate(-50%, -50%);
      width: 140%;
      z-index: -1;
      @include pseudo;
    }
  }
}
</style>
