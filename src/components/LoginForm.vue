<template>
  <form @submit.prevent>
    <div class="inputs">
      <fieldset>
        <legend>Username</legend>
        <my-input v-model="username" type="text" />
      </fieldset>
      <fieldset>
        <legend>Password</legend>
        <my-input v-model="password" type="text" />
      </fieldset>
    </div>
    <div class="commandButton">
      <my-button type="button" @click="register">register</my-button>
      <my-button type="button" @click="login">login</my-button>
    </div>
  </form>
</template>

<script>
import MyButton from "@/components/UI/MyButton.vue";
import MyInput from "@/components/UI/MyInput.vue";
import axios from "axios";

export default {
  components: { MyInput, MyButton },
  data() {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    register() {
      axios.post("http://localhost:8081/api/register", {
        username: this.username,
        password: this.password,
      });
    },
    login() {
      axios
        .post("http://localhost:8081/api/login", {
          username: this.username,
          password: this.password,
        })
        .then((res) => {
          localStorage.token = res.data.jwtToken;
          this.$router.push({ name: "main" });
        });
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

.button {
  width: 150px;
  font-size: 20px;
}
</style>
