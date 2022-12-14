<template>
  <div id="mainapp">
    <nav>Logo</nav>

    <section>
      <div
        class="slideVideo"
        v-for="videoContent in videosText"
        :key="videoContent"
      >
        <!-- The video -->
        <video :key="video" autoplay muted loop id="myVideo">
          <source :src="video" type="video/mp4" />
        </video>

        <!-- Optional: some overlay text to describe the video -->
        <div class="content">
          <h1>{{ videoContent.title }}</h1>
          <p>{{ videoContent.text }}</p>
        </div>
      </div>

      <a href="#slider" class="btn btn-bottom">
        <i class="fa fa-angle-down"></i>
      </a>
    </section>

    <Slider :images="images" :intervalDuration="slideDuration" />
  </div>
</template>

<script>
import Slider from "./slider/Slider.vue";
export default {
  components: {
    Slider,
  },
  data() {
    return {
      video: "http://www.w3schools.com/html/mov_bbb.mp4",
      videosText: [
        {
          id: 0,
          title: "LOREM IPSUM DOLOR",
          text: "Lorem ipsum dolor sit amet, consectetuer adipiscing elit.",
        },
      ],

      images: [
        {
          id: 0,
          url: "/images/image1.jpg",
          title: "DONEC NEC JUSTO",
          link: "DISCOVER MORE",
          class: "large",
        },
      ],

      imagesTab: [
        {
          id: 1,
          url: "/images/image2.jpg",
          title: "DONEC NEC JUSTO",
          link: "DISCOVER MORE",
          class: "tab",
        },
      ],
      imagesMobile: [
        {
          id: 2,
          url: "/images/image3.jpg",
          title: "DONEC NEC JUSTO",
          link: "DISCOVER MORE",
          class: "mobile",
        },
      ],

      slideDuration: 4000,
    };
  },
};
</script>

<style lang="scss">
</style>
