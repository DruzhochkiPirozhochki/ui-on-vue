<template>
  <v-container class="col-8">
    <HEADER></HEADER>
    <v-card>
      <v-card-title>
        Регистрация
      </v-card-title>
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
import HEADER from "./header.vue";
const qs = require("querystring");
export default {
  name: "SignUp",components: {
    HEADER,
  },
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
        .then((response) => {
          console.log(response.data);
          AXIOS.interceptors.request.use(function (config) {
            const token = response.data.value;
            config.headers.AuthorFization = "Bearer " + token;
            return config;
          });

          self.$router.push("/");
        })
        .catch((err) => {
          console.log(err);
        });
    },
    redirectToLogin() {
      this.$router.push("/signIn");
    },
  },
};
</script>

<style scoped>
</style>
