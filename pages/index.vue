<template>
  <h1>Hello would!!!</h1>
  <ul>
    <li v-for="user in users" :key="user.id">
      <div>{{ user.name }}</div>
      <div>{{ user.email }}</div>
    </li>
  </ul>
</template>

<script setup lang="ts">
import axios from 'axios'

interface Address {
  street: string
  suite: string
  city: string
  zipcode: string
  geo: {
    lat: string
    lng: string
  }
}

interface User {
  id: number
  name: string
  username: string
  email: string
  address: Address
  phone: string
  website: string
  company: {
    name: string
    catchPhrase: string
    bs: string
  }
}

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
