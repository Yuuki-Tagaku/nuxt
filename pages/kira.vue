<script setup lang="ts">
import axios from 'axios'

import { Album } from '~~/types/album'

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

<template>
  <h1>CHINCHIN!!!!!</h1>
  <ul>
    <li v-for="album in albums" :key="album.id">{{ album.title }}</li>
  </ul>
</template>
