<template>
  <header>
    <router-link to="/">Home</router-link> |
    <template v-if="isUserLogin">
      <span>{{ $store.state.username }}</span> |
      <button type="button" @click="logoutUser">Logout</button>
    </template>
    <template v-else>
      <router-link to="/login">로그인</router-link> |
      <router-link to="/signup">회원가입</router-link>
    </template>
  </header>
</template>

<script>
export default {
  computed: {
    isUserLogin() {
      return this.$store.getters.isLogin;
    }
  },
  methods: {
    logoutUser() {
      this.$store.commit("clearUsername");
      this.$router.push("/");
    }
  }
};
</script>

<style></style>
