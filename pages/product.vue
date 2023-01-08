<template>
  <ul>
    <li v-for="comment in comments" :key="comment.id">
      <div>{{ comment.name }}</div>
      <div>{{ comment.email }}</div>
    </li>
  </ul>
</template>

<script setup lang="ts">
import axios from 'axios'

interface Comment {
  postId: number
  id: number
  name: string
  email: string
  body: string
}

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
