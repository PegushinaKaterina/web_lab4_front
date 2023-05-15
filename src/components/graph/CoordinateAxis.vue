<template>
  <g id="axis-x" class="axis">
    <my-line :x="x" :y="y" :dx="length / 2" :dy="0"></my-line>
    <my-line
      v-for="i in k"
      :x="(length / k) * i"
      :y="y"
      :dx="0"
      :dy="d"
    ></my-line>
    <line
      :x1="x + length / 2"
      :y1="y"
      :x2="x + length / 2 - d"
      :y2="y + d"
    ></line>
    <line
      :x1="x + length / 2"
      :y1="y"
      :x2="x + length / 2 - d"
      :y2="y - d"
    ></line>
  </g>
  <g id="axis-y" class="axis">
    <my-line :x="x" :y="y" :dx="0" :dy="length / 2"></my-line>
    <my-line
      v-for="i in k"
      :x="x"
      :y="(length / k) * i"
      :dx="d"
      :dy="0"
    ></my-line>
    <line
      :x1="x"
      :y1="y - length / 2"
      :x2="x + d"
      :y2="y - length / 2 + d"
    ></line>
    <line
      :x1="x"
      :y1="y - length / 2"
      :x2="x - d"
      :y2="y - length / 2 + d"
    ></line>
  </g>
  <text
    v-for="i in k"
    :x="(length / k) * i"
    :y="y + 3 * d"
    text-anchor="middle"
  >
    {{ -r + ((i - 1) * r) / 2 }}
  </text>
  <text v-for="i in k" :x="x + (d * 3) / 2" :y="(length / k) * i + d / 2">
    {{ r - ((i - 1) * r) / 2 }}
  </text>
</template>

<script>
import MyLine from "@/components/graph/MyLine.vue";

export default {
  components: { MyLine },
  props: {
    x: Number,
    y: Number,
    length: Number,
    k: Number,
    d: Number,
    r: Number,
  },
  name: "coordinate-axis",
};
</script>

<style scoped>
line {
  stroke-width: 1.5px;
  stroke: black;
}
text {
  fill: black;
}
</style>
