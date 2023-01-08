<script setup lang="ts">
import axios from 'axios'

import { User } from '~~/types/user'

const users = ref<User[]>([])
const isLoading = ref(true)

const fetchUsers = async () => {
  const resData = await axios.get('https://jsonplaceholder.typicode.com/users')
  return resData.data
}

onMounted(async () => {
  try {
    isLoading.value = true
    users.value = await fetchUsers()
  } finally {
    isLoading.value = false
  }
})
</script>

<template>
  <h1>Hello world!!!</h1>
  <h2 v-if="isLoading === true">loading...</h2>
  <ul v-if="isLoading === false">
    <li v-for="user in users" :key="user.id">
      <div>{{ user.name }}</div>
      <div>{{ user.email }}</div>
    </li>
  </ul>
</template>
