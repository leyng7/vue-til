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
    <div>
      <label for="nickname">nickname: </label>
      <input type="text" name="nickname" id="nickname" v-model="nickname" />
    </div>
    <button type="submit" v-bind:disabled="!isFormValid">회원 가입</button>
    <p>{{ logMessage }}</p>
  </form>
</template>

<script>
import { registerUser } from "@/api";
import { validateEmail } from "@/utils/validation";

export default {
  data() {
    return {
      // form values
      username: "",
      password: "",
      nickname: "",
      // log
      logMessage: ""
    };
  },
  computed: {
    isFormValid() {
      return validateEmail(this.username) && this.password && this.nickname;
    }
  },
  methods: {
    async submitForm() {
      const { data } = await registerUser({
        username: this.username,
        password: this.password,
        nickname: this.nickname
      });
      this.logMessage = `${data.nickname} 님이 가입되었습니다.`;
      this.initForm();
    },
    initForm() {
      this.username = "";
      this.password = "";
      this.nickname = "";
    }
  }
};
</script>

<style></style>
