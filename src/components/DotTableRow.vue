<template>
  <div class="dotTableRow">
    <div class="dotRowElem dotRowShortElem">{{ dot.x }}</div>
    <div class="dotRowElem dotRowShortElem">{{ dot.y }}</div>
    <div class="dotRowElem dotRowShortElem">{{ dot.r }}</div>
    <div class="dotRowElem dotRowNormalElem">{{ dot.result }}</div>
    <div class="dotRowElem dotRowLongElem">{{ dot.checkTime }}</div>
    <div class="dotRowElem dotRowLongElem">{{ dot.computationTime }}</div>
  </div>
</template>

<script>
export default {
  name: "dot-table-row",
  props: {
    dot: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped>
.dotTableRow {
  box-sizing: border-box;
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  color: white;
  text-align: center;
}
.dotRowShortElem {
  width: 5%;
}
.dotRowNormalElem {
  width: 25%;
}
.dotRowLongElem {
  width: 30%;
}
</style>
