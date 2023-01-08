<script setup lang="ts">
import axios from 'axios'

import { Todo } from '~~/types/todo'

const todos = ref<Todo[]>([])

onMounted(async () => {
  const fetchTodos = async () => {
    const resData = await axios.get(
      'https://jsonplaceholder.typicode.com/todos'
    )
    return resData.data
  }
  todos.value = await fetchTodos()
  console.log('res', todos.value)
})
</script>

<template>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.title }}
    </li>
  </ul>
</template>
