<template>
  <div class="custom-slider w-full">
    <div class="custom-slider-outer">
      <div class="custom-slider-inner">
        <div class="custom-slider-wrap flex items-center justify-center">
          <div
            :class="current == 0 ? 'inactive' : null"
            @click="slide(-1)"
            class="custom-slider-btns custom-slider-btn--prev cursor-pointer"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-12 w-12"
              fill="none"
              viewBox="0 0 24 24"
              stroke="#fff"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M15 19l-7-7 7-7"
              />
            </svg>
          </div>
          <div class="flex-auto custom-slider-track">
            <ul class="custom-slider-slides-wrap" ref="slider-track">
              <li
                ref="slider-image"
                class="custom-slider-slide"
                v-for="(img, index) in images"
                :key="index + 'slide'"
              >
                <div class="custom-slider-slide-inner">
                  <div class="custom-slider-slide-img">
                    <img :src="img" alt="slider" />
                  </div>
                  <p class="custom-slider-slide-text">
                    {{ `Car ${index + 1}` }}
                  </p>
                </div>
              </li>
            </ul>
          </div>
          <div
            :class="
              images.length - slidesToshow - 1 < current ? 'inactive' : null
            "
            @click="slide(1)"
            class="custom-slider-btns custom-slider-btn--next cursor-pointer"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-12 w-12"
              fill="none"
              viewBox="0 0 24 24"
              stroke="#fff"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M9 5l7 7-7 7"
              />
            </svg>
          </div>
        </div>
        <ul class="custom-slider-pagi flex mt-4 justify-center">
          <li
            class="mx-1"
            :class="{ active: index == current }"
            v-for="(img, index) in images.slice(
              0,
              images.length - slidesToshow + 1
            )"
            :key="index + 'pagi'"
          ></li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import _ from "lodash";
import img1 from "../assets/images/nsx.jpg";
import img2 from "../assets/images/s2000.jpg";
import img3 from "../assets/images/type-r.jpg";
export default {
  data() {
    return {
      images: [img1, img2, img3, img1, img2, img3, img1, img2, img3],
      current: 0,
      direction: 1,
      slidesToshow: 3,
      transitionName: "fade",
      show: false,
    };
  },
  name: "Slider",
  mounted() {
    this.$nextTick(() => {
      this.$refs["slider-image"].forEach((item) => {
        item.style.width = 100 / this.slidesToshow + "%";
      });
    });
  },
  methods: {
    slide: _.debounce(
      function (direction) {
        let style = window.getComputedStyle(this.$refs["slider-track"]);
        let contWidth =
          this.$refs["slider-track"].getBoundingClientRect().width;
        let matrix =
          style.transform || style.webkitTransform || style.mozTransform;
        let currentTranslate = (+matrix.split(", ")[4] / contWidth) * 100;
        this.$refs["slider-track"].style.transform = `translateX(${
          currentTranslate + direction * -33.333
        }%)`;
        this.current += direction;
      },
      500,
      { leading: true, trailing: true }
    ),
  },
};
</script>
<style scoped>
</style>

