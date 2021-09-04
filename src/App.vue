<template>
  <div
    id="app"
    class="
      flex
      items-center
      justify-center
      bg-gradient-to-r
      p-6
      from-purple-400
      via-pink-500
      to-red-500
      min-h-screen
    "
  >
    <slider></slider>
  </div>
</template>

<script>
import Slider from "./components/slider.vue";
export default {
  name: "app",
  components: {
    Slider,
  },
  mounted() {},
};
</script>

