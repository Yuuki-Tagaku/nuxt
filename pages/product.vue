<script setup lang="ts">
import axios from 'axios'

import { Comment } from '~~/types/comment'

const comments = ref<Comment[]>([])

onMounted(async () => {
  const fetchComments = async () => {
    const resData = await axios.get(
      'https://jsonplaceholder.typicode.com/comments'
    )
    return resData.data
  }
  comments.value = await fetchComments()
  console.log('comments', comments.value)
})
</script>

<template>
  <ul>
    <li v-for="comment in comments" :key="comment.id">
      <div>{{ comment.name }}</div>
      <div>{{ comment.email }}</div>
    </li>
  </ul>
</template>
