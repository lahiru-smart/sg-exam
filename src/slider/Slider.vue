<template>
  <section id="slider">
    <Slides :image="images[chosenImage]" />

    <div class="controls">
      <div class="squares">
        <div class="active"></div>
        <div v-for="i in 3" :key="i"></div>
      </div>
    </div>
  </section>
</template>

<script>
import Slides from "./Slides.vue";
export default {
  components: {
    Slides,
  },
  props: ["images", "intervalDuration"],
  data() {
    return {
      chosenImage: 0,
      intervalObject: null,
      pauseplayToggle: false, //false - play, true - pause
    };
  },
  methods: {
    squares(id) {
      this.chosenImage = id;
      clearInterval(this.intervalObject);
      this.setIntervalSlider("right");
      this.pauseplayToggle = false;
    },
    arrowLeft() {
      clearInterval(this.intervalObject);
      this.moveLeft();
      this.setIntervalSlider("left");
    },
    arrowRight() {
      clearInterval(this.intervalObject);
      this.moveRight();
      this.setIntervalSlider("right");
    },
    moveLeft() {
      var flag = this.chosenImage;
      flag--;
      if (flag < 0) {
        flag = this.images.length - 1;
      }
      this.chosenImage = flag;
      this.pauseplayToggle = false;
    },
    moveRight() {
      var flag = this.chosenImage;
      flag++;
      if (flag >= this.images.length) {
        flag = 0;
      }
      this.chosenImage = flag;
      this.pauseplayToggle = false;
    },
    pauseplay(action) {
      console.log("in pauseplay method ", action);
      if (action == "play") {
        this.arrowRight();
        this.pauseplayToggle = false;
      } else if (action == "pause") {
        clearInterval(this.intervalObject);
        this.pauseplayToggle = true;
      }
    },
    setIntervalSlider(direction) {
      var self = this;
      this.intervalObject = setInterval(() => {
        if (direction == "right") {
          self.moveRight();
        } else if (direction == "left") {
          self.moveLeft();
        }
      }, this.intervalDuration);
    },
  },
  created() {
    this.setIntervalSlider("right");
  },
};
</script>




