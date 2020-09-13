<template>
  <v-app>
    <v-app-bar app dark src="https://cdn.vuetifyjs.com/images/backgrounds/vbanner.jpg">
      <v-avatar class="logo" tile>
        <v-img contain src="../public/logo.jpg"></v-img>
      </v-avatar>
      <v-spacer />
      <template v-if="this.$store.getters.getToken != ''">
        <v-btn class="btn" disabled text>
          <v-icon class="icon">mdi-account</v-icon>
          {{this.$store.state.username}}
        </v-btn>
        <v-btn class="btn" href="/" text>
          <v-icon class="icon">mdi-send</v-icon>Отправить
        </v-btn>
        <v-btn class="btn" href="/troubles" text>
          <v-icon class="icon">mdi-cog</v-icon>Проблемы
        </v-btn>
        <v-btn class="btn" @click="logout" text>
          <v-icon class="icon">mdi-logout</v-icon>Выйти
        </v-btn>
      </template>
      <template v-else>
        <v-btn class="btn" href="/signUp" text>
          <v-icon class="icon">mdi-account-plus</v-icon>Регистрация
        </v-btn>
        <v-btn class="btn" href="/signIn" text>
          <v-icon class="icon">mdi-login</v-icon>Вход
        </v-btn>
      </template>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from "./components/HelloWorld";

export default {
  name: "App",

  components: {
    HelloWorld,
  },

  data: () => ({
    //
  }),
  methods: {
    logout() {
      this.$store.dispatch("logout");
      this.$router.push("/signIn");
    },
  },
};
</script>

<style scoped>
.btn {
  font-size: 0.75vw !important;
}
</style>
