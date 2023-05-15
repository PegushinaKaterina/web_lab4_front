<template>
  <svg id="svg" class="svg" viewBox="0 0 300 300" @click="createDot">
    <g class="figures">
      <rect x="50" y="150" width="100" height="100" class="square"></rect>
      <polyline points="150,150 150,250 200,150 150,150"></polyline>
      <path d="M150,150 h-100 A100,100 90 0,1 150,50 z"></path>
    </g>
    <coordinate-axis
      :x="150"
      :y="150"
      :length="250"
      :d="10"
      :k="5"
      :r="r"
    ></coordinate-axis>
    <circle class="circle" r="0" cx="50" cy="50" fill="black" />
    <circle class="circle" r="0" cx="150" cy="150" fill="black" />
    <circles :x="150" :y="150" :r="r" :circles="circles"></circles>
  </svg>
</template>

<script>
import Circles from "@/components/graph/Circles.vue";
import CoordinateAxis from "@/components/graph/CoordinateAxis.vue";
import axios from "axios";

export default {
  name: "my-graph",
  data() {
    return {
      dot: {
        x: 0,
        y: 0,
      },
    };
  },
  components: { CoordinateAxis, Circles },
  props: {
    r: Number,
    circles: {
      type: Array,
    },
  },
  methods: {
    createDot() {
      let circle = document.querySelectorAll(".circle");
      let r =
        Math.round(circle[1].getBoundingClientRect().x) -
        Math.round(circle[0].getBoundingClientRect().x);
      let x = event.clientX - Math.round(circle[1].getBoundingClientRect().x);
      let y = Math.round(circle[1].getBoundingClientRect().y) - event.clientY;
      this.dot.x = (this.r * x) / r;
      this.dot.y = (this.r * y) / r;
      if (this.dot.y >= -5 && this.dot.y <= 5) {
        axios
          .post(
            "http://localhost:8081/api/dots",
            {
              x: this.dot.x,
              y: this.dot.y,
              r: this.r,
            },
            {
              headers: {
                Authorization: "Bearer " + localStorage.token,
              },
            }
          )
          .finally(() => {
            this.$emit("create2");
          });
      }
    },
  },
};
</script>

<style scoped>
.figures {
  fill: #a6998e;
  stroke: black;
  stroke-width: 1.5px;
}
</style>
