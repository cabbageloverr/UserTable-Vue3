<script setup lang="ts">
import CardStyle from "./CardStyle.vue"
import type { User} from "@/interface/user"

const props = withDefaults(defineProps<{
  user : User
}>(),{
    
}) 

</script>
<template>
<div>
<CardStyle class="card-user">
    <p class="name">{{ user.name }}</p>
    <p class="phone">
      Phone: {{ user.phones }}
      <span  alt="plsplspls" class="border tiny" v-if="user.phones.length > 1">
        +{{ user.phones.length - 1 }}</span
      >
    </p>
    <p class="email">Email: {{ user.email }}</p>
  </CardStyle></div>

</template >

<style >

</style>
