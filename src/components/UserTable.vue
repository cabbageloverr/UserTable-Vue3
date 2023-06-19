<script setup lang="ts">
import { ref, watch, reactive, onMounted  } from "vue";
import type { User } from "@/interface/user";
import CardStyle from "./CardStyle.vue";
import CardUser from "./CardUser.vue";
import Input from "./input/Input.vue"

const props = withDefaults(
  defineProps<{
    users: User[]
    user : User
    text?: string;
  }>(),
  {
    text: ''
  }
);

// const text = ref<string>('');
const userlist = ref<string[]>([])



function findInArr(array: string, keyword: string) {
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
      findInArr(item.phones, props.text) ||
      item.name.toLowerCase().includes(props.text.toLowerCase()) ||
      item.email.toLowerCase().includes(props.text.toLowerCase())
  );
};

watch(
  () => props.text,
  () => {
    userlist.value = search();
  },
  { immediate: true }
);


onMounted(() => {
  search();
})
</script>

<template>
  <div>
  
  <CardStyle class="container con1">
    <Input> </Input>
    <h3 class="result">
      Result <span class="text_gray">({{ userlist.length }})</span>
    </h3>

    <div class="row">
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

<style>
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

.s_bt {
  margin-left: 12px;
  padding: 2px 12px;
  width: 110px;

  background: #5119f0 !important;
  border-radius: 4px !important;
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
  height: 88px;

  line-height: 10px !important;
}

.name {
  font-weight: bold;
  font-size: 14px;
}

.phone {
  font-size: 12px;
  color: rgb(140, 145, 150);
}

.email {
  font-size: 12px;
  color: rgb(140, 145, 150);
  width: 200px;
}

.tiny {
  border-radius: 2px;
  justify-content: center;
  align-items: center;
  padding: 0px 4px 1px;
  background: #efedff;
  border-radius: 4px;
  color: #5119f0;
}

</style>
