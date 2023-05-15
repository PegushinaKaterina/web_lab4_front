<template>
  <my-circle
    v-for="circle in circles"
    :x="x"
    :y="y"
    :r="r"
    :cx="circle.x"
    :cy="circle.y"
    :radius="circle.radius"
    :stroke="circle.colorStroke"
    :strokeWidth="2"
    :fill="circle.colorFill"
  ></my-circle>
</template>

<script>
import MyCircle from "@/components/graph/MyCircle.vue";
export default {
  components: { MyCircle },
  props: {
    x: Number,
    y: Number,
    circles: {
      type: Array,
    },
    r: Number,
  },
}
</script>

<style lang="scss" scoped>

</style>