<template>
  <v-container class="col-8">
    <v-card>
      <v-card-title>Вход</v-card-title>
      <v-card-text>
        <v-text-field outlined placeholder="Имя пользователя" type="mail" v-model="username"></v-text-field>
        <v-text-field outlined placeholder="Пароль" type="password" v-model="password"></v-text-field>
        <v-card-actions>
          <v-btn dark color="blue" @click="signIn()">Войти</v-btn>
          <v-spacer />
          <v-btn outlined @click="redirectToSignUp()">Зарегистрироваться</v-btn>
        </v-card-actions>
      </v-card-text>
    </v-card>
  </v-container>
</template>

<style scoped>
.login-btn {
  width: 100%;
}

.login-card {
  padding: 10px;
}
</style>
<script>
import { AXIOS } from "../main";

export default {
  name: "SignIn",
  data: () => ({
    username: "",
    password: "",
  }),
  methods: {
    signIn() {
      let self = this;
      AXIOS.post("/signIn", {
        username: self.username,
        password: self.password,
      })
        .then((response) => {
          console.log(response.data);
          AXIOS.interceptors.request.use(function (config) {
            const token = response.data.value;
            config.headers.Authorization = "Bearer " + token;

            return config;
          });
          self.$store
            .dispatch("signIn", {
              token: response.data.value.token,
              id: response.data.id,
              username: response.data.username,
            })
            .then(() => {
              self.$router.push("/");
            });
        })
        .catch((err) => {
          console.log(err);
        });
    },
    redirectToSignUp() {
      this.$router.push("/signUp");
    },
  },
};
</script>