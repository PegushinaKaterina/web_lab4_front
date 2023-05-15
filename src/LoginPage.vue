<template>
  <div class="app">
    <div class="header">
      <h2>Лабораторная работа №4</h2>
    </div>
    <div class="main">
      <login-form class="form appElement" />
    </div>
  </div>
</template>

<script>
import LoginForm from "@/components/LoginForm.vue";

export default {
  components: {
    LoginForm,
  },
  name: "App",
  data() {
    return {
      username: "",
      password: "",
    };
  },
};
</script>

<style scoped>
*:global(*) {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  border-radius: 7px;
  background-color: #d7d4c9;
  font-family: "Courier New";
  font-weight: bolder;
  color: black;
}
.app {
  font-size: 20px;
  width: 100%;
  padding: 10px;
  display: flex;
  flex-direction: column;
  box-sizing: border-box;
}
.main {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
}

.form {
  width: 40%;
  height: 300px;
  margin: 10px;
  padding: 20px;
  border: 1.5px solid black;
  display: flex;
  flex-direction: column;
}

.header {
  width: 100%;
  text-align: center;
  font-size: 45px;
  margin: 50px 0px 50px 0px;
}
</style>
