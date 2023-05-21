<template>
  <form @submit.prevent="submitForm">
    <div>
      <label for="username">id: </label>
      <input type="text" name="username" id="username" v-model="username" />
    </div>
    <div>
      <label for="password">pw: </label>
      <input type="text" name="password" id="password" v-model="password" />
    </div>
    <button v-bind:disabled="!isUsernameValid || !password">로그인</button>
    <p>{{ logMessage }}</p>
  </form>
</template>

<script>
import { loginUser } from "@/api";
import { validateEmail } from "@/utils/validation";

export default {
  data() {
    return {
      // form values
      username: "",
      password: "",
      // log
      logMessage: ""
    };
  },
  computed: {
    isUsernameValid() {
      return validateEmail(this.username);
    }
  },
  methods: {
    async submitForm() {
      try {
        const { data } = await loginUser({
          username: this.username,
          password: this.password
        });
        this.logMessage = `${data.user.nickname} 님 환영합니다.`;
        this.$store.commit("setUsername", data.user.username);
        this.$router.push("/");
      } catch (e) {
        this.logMessage = "해당하는 회원이 없습니다.";
      } finally {
        this.initForm();
      }
    },
    initForm() {
      this.username = "";
      this.password = "";
    }
  }
};
</script>

<style></style>
