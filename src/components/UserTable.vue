<script setup lang="ts">
import { ref, watch, reactive, onMounted, computed  } from "vue";
import type { User } from "@/interface/user";
import CardStyle from "./CardStyle.vue";
import CardUser from "./CardUser.vue";
import Input from "./input/Input.vue"
import Button from "./button/Button.vue"
const props = withDefaults(
  defineProps<{
    users: User[]
    user : User
  }>(),
  {}
);

const userlist = ref<User[]>([])
const text = ref('')


function findInArr(array: string[], keyword: string) {
  for (let i = 0; i < array.length; i++) {
    const item = array[i];
    if (item.startsWith(keyword)) {
      return true;
    }
  }
  return false;
}


  const search = () => {
    return props.users.filter(
      (item) =>
        findInArr(item.phones, text.value) ||
        item.name.toLowerCase().includes(text.value.toLowerCase()) ||
        item.email.toLowerCase().includes(text.value.toLowerCase())
    );
  };


watch(
  () => text.value,
  () => {
    console.log(userlist.value)
    userlist.value = search();
    
  },{
    immediate : true
  }
);


onMounted(() => {
  console.log("onmountes")
  search()
  console.log("search")
});

</script>

<template>
  <div>
  
  <CardStyle class="container con1">
    
  <Input v-model="text" />
  <Button @click="search" v-model="text"></Button>
    <h3 class="result">
      Result <span class="text_gray">({{ userlist.length }})</span>
    </h3>

    <div class="row gap-4">
      <CardUser
        :user="user"
        v-for="user in userlist"
        :key="user.name"
        class="col-3 user-table"
      >
      </CardUser>
    </div>
 
  </CardStyle>
</div>
</template>

<style scoped>
.con1 {
  position: absolute;
  width: 1096px;
  height: auto;
  left: 5%;
  top: 86px;
  background: #ffffff;
  box-shadow: 1px 1px 6px rgba(69, 73, 87, 0.12) !important;
  border-radius: 8px;
  padding: 24px !important;
}



.s_bt:hover {
  background-color: rgb(135, 108, 230) !important;
}

.result {
  margin-top: 1rem;
  font-weight: bold;
}

/* th {
  background-color: rgb(233, 232, 241) !important ;
} */

.row {
  margin-left: 0 !important;
}
.text_gray {
  color: #646d78;
}

.user-table {
  width: 22% !important;
 height: 88px !important;

  line-height: 5px !important;
}




</style>
