<script setup lang="ts">
import axios from 'axios'

import { Post } from '~~/types/post'

// refは状態管理
const posts = ref<Post[]>([])

// onMountedはVueのtemplateタグの中身がDOMを介してHTMLに反映された後に発火するメソッド
onMounted(async () => {
  const fetchPosts = async () => {
    const resData = await axios.get(
      'https://jsonplaceholder.typicode.com/posts'
    )
    return resData.data
  }
  posts.value = await fetchPosts()
  console.log('posts', posts.value)
})
</script>

<template>
  <h1>MANMAN!!!!!</h1>
  <ul>
    <li v-for="post in posts" :key="post.id">
      <div>{{ post.title }}</div>
      <div>{{ post.body }}</div>
    </li>
  </ul>
</template>
