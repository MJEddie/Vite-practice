<template>
  <div id="loginPage" class="bg-yellow">
    <div class="container loginPage vhContainer">
      <div class="side">
        <a href="#"
          ><img
            class="logoImg"
            src="https://raw.githubusercontent.com/hexschool/2022-web-layout-training/main/todolist/logo.png"
            alt=""
        /></a>
        <img
          class="d-m-n"
          src="https://raw.githubusercontent.com/hexschool/2022-web-layout-training/main/todolist/img.png"
          alt="workImg"
        />
      </div>
      <div>
        <form class="formControls" action="index.html">
          <h2 class="formControls_txt">最實用的線上代辦事項服務</h2>
          <label class="formControls_label" for="email">Email</label>
          <input
            class="formControls_input"
            type="text"
            id="email"
            name="email"
            v-model="email"
            placeholder="請輸入 email"
            required
          />
          <span v-if="email.value === ''">此欄位不可留空</span>
          <label class="formControls_label" for="pwd">密碼</label>
          <input
            class="formControls_input"
            type="password"
            name="pwd"
            id="pwd"
            v-model="password"
            placeholder="請輸入密碼"
            required
          />
          <input
            class="formControls_btnSubmit"
            type="button"
            @click="handleLogin"
            value="登入"
          />
          <Router-link class="formControls_btnLink" to="/register"
            >註冊帳號</Router-link
          >
        </form>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";
import { login } from "@/utils/api.js";

const router = useRouter();

const email = ref("");
const password = ref("");

const handleLogin = async () => {
  try {
    const res = await login(email.value, password.value);
    const { token, exp } = res.data;
    document.cookie = `vue3-todolist-token=${token}; expires=${exp}`;

    alert("登入成功");
    router.push("/todolist");
  } catch (err) {
    alert(`發生錯誤: ${err.response.data.message}`);
  }
};
</script>
