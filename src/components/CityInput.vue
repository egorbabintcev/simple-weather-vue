<template>
  <div class="city-input">
    <form class="city-input__form" @submit.prevent="">
      <input
        type="text"
        placeholder="Weather in..."
        @input="handler"
        :value="modelValue"
      />
    </form>
  </div>
</template>

<script>
import _ from "lodash";

export default {
  name: "CityInput",
  props: {
    modelValue: String,
  },
  emits: ["update:modelValue", "afterInput"],
  methods: {
    handler(e) {
      this.$emit("update:modelValue", e.target.value);
      this.debouncedCb();
    },
    debouncedCb: _.debounce(function () {
      this.$emit("afterInput");
    }, 500),
  },
};
</script>

<style lang="scss">
@import "@/assets/sass/utils/functions";

.city-input {
  margin-bottom: rem(40);

  &__form {
    input {
      border: rem(1) solid hsl(0, 0%, 80%);
      color: #2c3e50;
      letter-spacing: 0.025em;
      padding: rem(10) rem(20);
      width: 100%;
      font: {
        size: rem(28);
        style: italic;
        weight: 400;
      }
    }
  }
}
</style>
