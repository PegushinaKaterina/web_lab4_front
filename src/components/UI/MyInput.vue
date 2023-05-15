<template>
  <input
    :value="modelValue"
    class="input elementForm"
    @input="updateInput"
  />
</template>

<script>
export default {
  name: "my-input",
  props: {
    modelValue: [Number, String],
  },
  methods: {
    updateInput(event) {
      this.$emit("update:modelValue", event.target.value);
    },
  },
};
</script>

<style scoped>
.input {
  width: 100%;
  background-color: #836c7b;
  padding: 7px;
  border: 1.5px solid black;
  font-size: var(--element-form-text-size);
}
</style>
