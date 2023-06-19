<script setup lang="ts">
import { ref, reactive } from "vue";


// const text = reactive({ word: "" });
const text = "";

</script>
<template>
  <input v-model="text" type="text" placeholder="Search"     />
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
