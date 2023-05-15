<template>
  <div class="dotTable">
    <div class="a">
      <dot-table-row :dot="headerDot" class="dotTableHeader" />
      <dot-table-row v-for="dot in dots" :key="dot.id" :dot="dot" />
    </div>
    <my-button type="button" @click="cleanTable">Сбросить</my-button>
  </div>
</template>

<script>
import DotTableRow from "@/components/DotTableRow.vue";
import MyButton from "@/components/UI/MyButton.vue";

export default {
  components: { MyButton, DotTableRow },
  props: {
    headerDot: {
      type: Object,
      required: true,
    },
    dots: {
      type: Array,
    },
  },
  methods: {
    cleanTable() {
      this.$emit("clean");
    },
  },
};
</script>

<style scoped>
.a {
  height: 100%;
  overflow-y: scroll;
}
.dotTableHeader {
  background-color: #828670;
  border: 1.5px solid black;
  padding: 10px 0px 10px 0px;
  margin: 10px 0px 10px 0px;
}

.dotTableHeader :deep(div) {
  background-color: #828670;
  color: black;
}
</style>
