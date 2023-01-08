<script setup lang="ts">
import axios from 'axios'

import { User } from '~~/types/user'

const users = ref<User[]>([])

onMounted(async () => {
  const fetchUsers = async () => {
    const resData = await axios.get(
      'https://jsonplaceholder.typicode.com/users'
    )
    return resData.data
  }
  users.value = await fetchUsers()
  console.log('users', users.value)
})
</script>

<template>
  <h1>Hello would!!!</h1>
  <ul>
    <li v-for="user in users" :key="user.id">
      <div>{{ user.name }}</div>
      <div>{{ user.email }}</div>
    </li>
  </ul>
</template>
