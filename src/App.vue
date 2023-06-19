<script setup lang="ts">
import { ref } from "vue";
import UserTable from "./components/UserTable.vue";
import type { User } from "../src/interface/user";

const users = ref<User[]>([]);

async function getData() {
  const res = await fetch("http://localhost:3000/users");
  const finalRes = await res.json();
  users.value = finalRes;
}
getData();
</script>

<template>
  <div id="app">
    <!-- <HelloWorld/> -->
    <UserTable :users="users"></UserTable>
  </div>
</template>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  justify-content: center;
 
}
</style>
