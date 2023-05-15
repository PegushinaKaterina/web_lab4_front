<template>
  <form @submit.prevent>
    <div class="inputs">
      <fieldset>
        <legend>Значение X</legend>
        <my-select v-model="dot.x" :options="numberOptions" />
      </fieldset>
      <fieldset>
        <legend>Значение Y</legend>
        <my-input v-model="dot.y" type="number" max="5" min="-5" />
      </fieldset>
      <fieldset>
        <legend>Значение R</legend>
        <my-select v-model="dot.r" :options="numberOptionsR" @change="changeR" />
      </fieldset>
    </div>
    <div class="commandButton">
      <my-button type="button" @click="resetForm">Сбросить</my-button>
      <my-button type="button" @click="createDot">Отправить</my-button>
    </div>
  </form>
</template>

<script>
import MyButton from "@/components/UI/MyButton.vue";
import MyInput from "@/components/UI/MyInput.vue";
import MySelect from "@/components/UI/MySelect.vue";
import axios from "axios";

export default {
  components: { MySelect, MyInput, MyButton },
  data() {
    return {
      dotRequestFish: false,
      dot: {
        x: 0,
        y: 0,
        r: 1,
      },
      numberOptions: [
        { value: -5, name: "-5" },
        { value: -4, name: "-4" },
        { value: -3, name: "-3" },
        { value: -2, name: "-2" },
        { value: -1, name: "-1" },
        { value: 0, name: "0" },
        { value: 1, name: "1" },
        { value: 2, name: "2" },
        { value: 3, name: "3" },
      ],
      numberOptionsR: [
        { value: 1, name: "1" },
        { value: 2, name: "2" },
        { value: 3, name: "3" },
      ],
    };
  },
  methods: {
    createDot() {
      if (this.dot.y >= -5 && this.dot.y <= 5) {
        axios
          .post(
            "http://localhost:8081/api/dots",
            {
              x: this.dot.x,
              y: this.dot.y,
              r: this.dot.r,
            },
            {
              headers: {
                Authorization: "Bearer " + localStorage.token,
              },
            }
          )
          .finally(() => {
            this.$emit("create");
          });
      };
    },
    resetForm() {
      this.dot = {
        x: 0,
        y: 0,
        r: 1,
      };
    },
    changeR() {
      this.$emit("changeR", this.dot.r);
    },
  },
};
</script>

<style scoped>
fieldset {
  margin-top: 15px;
  border: 1.5px solid black;
  padding: 10px;
}

.commandButton {
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
}
.inputs {
  height: 100%;
}
</style>
