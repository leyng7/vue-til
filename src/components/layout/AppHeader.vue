<template>
  <header>
    <router-link to="/">Home</router-link> |
    <template v-if="isUserLogin">
      <span>{{ $store.state.username }}</span> |
      <button type="button" @click="logoutUser">Logout</button>
      <button type="button" @click="testAxios"></button>
    </template>
    <template v-else>
      <router-link to="/login">로그인</router-link> |
      <router-link to="/signup">회원가입</router-link>
    </template>
  </header>
</template>

<script>
import { test } from "@/api";

export default {
  computed: {
    isUserLogin() {
      return this.$store.getters.isLogin;
    }
  },
  methods: {
    logoutUser() {
      this.$store.commit("clearUsername");
      this.$store.commit("clearToken");
      this.$router.push("/");
    },
    testAxios() {
      test();
    }
  }
};
</script>

<style></style>
