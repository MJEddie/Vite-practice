<template>
  <div>
    <h2>註冊</h2>
    <input v-model="emailSignUp" placeholder="Email" />
    <input v-model="passwordSignUp" placeholder="Password" type="password" />
    <input v-model="nickname" placeholder="Nickname" type="text" />
    <button @click="signUp">Sign Up</button>
    <p>{{ messageSignUp }}</p>

    <h2>登入</h2>
    <input v-model="emailSignIn" placeholder="Email" type="email" />
    <input v-model="passwordSignIn" placeholder="Password" type="password" />
    <button @click="signIn">Sign In</button>
    <p>Token: {{ token }}</p>

    <h2>驗證</h2>
    <input v-model="tokenCheck" placeholder="Token" />
    <button @click="checkOut">Check Out</button>
    <p>{{ messageCheckOut }}</p>

    <h2>登出</h2>
    <input v-model="tokenSignOut" placeholder="Token" />
    <button @click="signOut">Sign Out</button>

    <hr />
    <h2>Todo list</h2>
    <div v-if="token">
      <input v-model="newTodo" placeholder="New Todo" />
      <button @click="addTodo">Add Todo</button>
      <ul>
        <li v-for="(todo, index) in todos" :key="index">
          {{ todo.content }} {{ todo.status ? "完成" : "未完成" }} |
          {{ todoEdit[todo.id] }}
          <input
            type="text"
            placeholder="更新值"
            @change="updateTodoEdit($event, todo.id)"
          />
          <button @click="deleteTodo(todo.id)">Delete</button>
          <button @click="updateTodo(todo.id)">Update</button>
          <button @click="toggleStatus(todo.id)">Toggle Status</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";

const requestUrl = "https://todolist-api.hexschool.io";

// 註冊
const emailSignUp = ref("");
const passwordSignUp = ref("");
const nickname = ref("");
const messageSignUp = ref("");

const signUp = async () => {
  try {
    const res = await axios.post(`${requestUrl}/users/sign_up`, {
      email: emailSignUp.value,
      password: passwordSignUp.value,
      nickname: nickname.value,
    });
    messageSignUp.value = "註冊成功. UID: " + res.data.uid;
  } catch (err) {
    messageSignUp.value = "註冊失敗:" + err.response.data.message;
  }
};

// 登入
const emailSignIn = ref("");
const passwordSignIn = ref("");
const token = ref("");

// 驗證
const tokenCheck = ref("");
const messageCheckOut = ref("");

// 登出
const tokenSignOut = ref("");
</script>
