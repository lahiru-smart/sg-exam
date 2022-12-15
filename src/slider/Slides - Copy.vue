<template>
  <transition-group name="fade" mode="out-in" tag="div" id="slides">
    <div class="slideParent" :key="image.id">
      <section>
        <div class="discoverText">
          <a href="#">{{ image.link }}</a>
        </div>
        <div
          class="slideImage"
          :class="image.class"
          :style="setBackgroundImage"
        >
          <div class="carouselWrap">
            <div class="slideTitle">
              {{ image.title }}
            </div>
            <carousel>
              <carousel-slide class="carousel-slider">
                <!-- <img :src="slide" :alt="slide" /> -->

                <div class="carousel-sec">
                  <div
                    class="carousel-box"
                    v-for="slide in slides"
                    :key="slide.id"
                  >
                    <div class="carousel-heading">{{ slide.title }}</div>
                    <div class="carousel-text">
                      {{ slide.text }}
                    </div>
                  </div>
                </div>
              </carousel-slide>
            </carousel>
          </div>
        </div>
      </section>
    </div>
  </transition-group>
</template>

<script>
import Carousel from "../../src/components/carousel/Carousel.vue";
import CarouselSlide from "../../src/components/carousel/CarouselSlide";
export default {
  data: () => ({
    slides: [
      {
        id: 0,
        title: "Heading",
        text: "Donec nec justo eget felis facilisis fermentum. Aliquam porttitor mauris sit amet orci.",
      },
      {
        id: 1,
        title: "Heading2",
        text: "Donec nec justo eget felis facilisis fermentum. aaaaa",
      },
      {
        id: 2,
        title: "Heading3",
        text: "Donec nec justo eget felis facilisis fermentum. aaaaa",
      },
      {
        id: 3,
        title: "Heading4",
        text: "Donec nec justo eget felis facilisis fermentum. aaaaa",
      },
      {
        id: 4,
        title: "Heading5",
        text: "Donec nec justo eget felis facilisis fermentum. aaaaa",
      },
    ],
    visibleSlide: 3,
  }),
  components: {
    Carousel: Carousel,
    CarouselSlide: CarouselSlide,
  },

  beforeMount() {
    window.addEventListener("resize", this.onResize.bind(this));
    this.handleResize();
  },
  beforeDestroy() {
    // don't forget to implement unsubscribe event.
    window.removeEventListener("resize", this.handleResize);
  },
  methods: {
    // when implementing this in production,
    // try wrap this method with debounce method first
    // because there will be users with a REALLY BAD PC out there.
    onResize() {
      if (window.innerWidth > 1440) {
        this.image.class = "large";
      } else if ((window.innerWidth < 1440) & (window.innerWidth > 600)) {
        this.image.class = "tab";
      } else if (window.innerWidth < 600) {
        this.image.class = "mobile";
      }
    },
  },

  props: ["image"],
  computed: {
    setBackgroundImage() {
      return { backgroundImage: "url(" + this.image.url + ")" };
    },
  },
};
</script>

<style lang="scss">
@import "style.scss";
</style>