<template>
  <ul>
    <li v-for="photo in photos" :key="photo.albumId">
      <div>{{ photo.title }}</div>
      <img :src="photo.thumbnailUrl" />
    </li>
  </ul>
</template>

<script setup lang="ts">
import axios from 'axios'

interface Photo {
  albumId: number
  id: number
  title: string
  url: string
  thumbnailUrl: string
}

const photos = ref<Photo[]>([])

onMounted(async () => {
  const fetchPhotos = async () => {
    const resData = await axios.get(
      'https://jsonplaceholder.typicode.com/photos?_start=0&_limit=10'
    )
    return resData.data
  }
  photos.value = await fetchPhotos()
  console.log('res', photos.value)
})
</script>
