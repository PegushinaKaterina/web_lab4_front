<template>
  <line :x1="x - dx" :y1="y - dy" :x2="x + dx" :y2="y + dy"></line>
</template>

<script>
export default {
  name: "my-line",
  props: {
    x: Number,
    y: Number,
    dx: Number,
    dy: Number,
  },
};
</script>

<style scoped>

</style>
