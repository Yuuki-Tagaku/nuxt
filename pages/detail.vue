<template>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.title }}
    </li>
  </ul>
</template>

<script setup lang="ts">
import axios from 'axios'

interface Todo {
  userId: number
  id: number
  title: string
  completed: boolean
}

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
