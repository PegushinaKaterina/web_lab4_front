<template>
  <circle :r="radius" :cx="x+2/3*x*cx/r" :cy="y-2/3*y*cy/r" :stroke="stroke" :strokeWidth="strokeWidth" :fill="fill" />
</template>

<script>
export default {
  name: "my-circle",
  props: {
    radius: Number,
    r: Number,
    x: Number,
    y: Number,
    cx: Number,
    cy: Number,
    stroke: String,
    strokeWidth: Number,
    fill: String,
  },
};
</script>

<style scoped>

</style>
