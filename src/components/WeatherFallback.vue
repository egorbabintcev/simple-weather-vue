<template>
  <div class="weather-fallback">
    <h3>City not found!</h3>
  </div>
</template>

<script>
export default {
  name: "WeatherFallback",
};
</script>

<style lang="scss">
@import "@/assets/sass/utils/functions";

.weather-fallback {
  align-items: center;
  display: flex;
  flex-direction: column;

  h3 {
    color: hsl(210, 29%, 35%);
    font: {
      size: rem(36);
      style: italic;
      weight: 700;
    }
  }
}
</style>
