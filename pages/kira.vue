<template>
  <h1>CHINCHIN!!!!!</h1>
  <ul>
    <li v-for="album in albums" :key="album.id">{{ album.title }}</li>
  </ul>
</template>

<script setup lang="ts">
import axios from 'axios'

interface Album {
  userId: number
  id: number
  title: string
}

const albums = ref<Album[]>([])

onMounted(async () => {
  const fetchAlbums = async () => {
    const resData = await axios.get(
      'https://jsonplaceholder.typicode.com/albums'
    )
    // console.log('getAlbums', albums.data)
    return resData.data
  }
  albums.value = await fetchAlbums()
  console.log('albums', albums.value)
})
</script>
