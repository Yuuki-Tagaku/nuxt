<script setup lang="ts">
import axios from 'axios'

import { Photo } from '~~/types/photo'

const photos = ref<Photo[]>([])
const isLoading = ref(true)

const fetchPhotos = async () => {
  const resData = await axios.get(
    'https://jsonplaceholder.typicode.com/photos?_start=0&_limit=10'
  )
  return resData.data
}

onMounted(async () => {
  try {
    isLoading.value = true
    photos.value = await fetchPhotos()
    console.log('res', photos.value)
  } finally {
    isLoading.value = false
  }
})
</script>

<template>
  <h2 v-if="isLoading === true">loading...</h2>
  <ul v-if="isLoading === false">
    <li v-for="photo in photos" :key="photo.albumId">
      <div>{{ photo.title }}</div>
      <img :src="photo.thumbnailUrl" />
    </li>
  </ul>
</template>
