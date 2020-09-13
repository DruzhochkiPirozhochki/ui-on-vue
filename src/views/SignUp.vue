<template>
  <v-container class="col-8">
    <v-card>
      <v-card-title>Регистрация</v-card-title>
      <v-card-text>
        <v-text-field outlined placeholder="Имя пользователя" type="text" v-model="username"></v-text-field>
        <v-text-field outlined placeholder="Почта" v-model="email" type="mail"></v-text-field>
        <v-text-field outlined placeholder="Пароль" v-model="password" type="password"></v-text-field>

        <v-card-actions>
          <v-btn dark color="blue" @click="signUp()">Зарегистрироваться</v-btn>
          <v-spacer />
          <v-btn outlined @click="redirectToLogin()">Войти</v-btn>
        </v-card-actions>
      </v-card-text>
    </v-card>
  </v-container>
</template>

<script>
import { AXIOS } from "../main";

const qs = require("querystring");
export default {
  name: "SignUp",
  data: () => ({
    username: "",
    email: "",
    password: "",
  }),
  methods: {
    signUp() {
      let self = this;
      AXIOS.post("/signUp", {
        username: this.username,
        email: this.email,
        password: this.password,
      })
      .catch((err) => {
        console.log(err);
      });
      this.redirectToLogin();
    },
    redirectToLogin() {
      this.$router.push("/signIn");
    },
  },
};
</script>

<style scoped>
</style>
