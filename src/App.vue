<template>
  <!-- <div>
    <h1>{{ message }}</h1>
  </div> -->
  <body data-spy="scroll" data-target="#scroll-spy">
  <Navbar/>
  <RouterView />
</body>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { RouterLink, RouterView } from 'vue-router'
import axios from 'axios'
import Navbar from './components/layouts/Navbar.vue';

// Define a ref to store the response message
const message = ref('Loading...')

// Fetch data from the Bun backend
const fetchData = async () => {
  try {
    const response = await axios.get('http://localhost:4000/api/hello')
    message.value = response.data.message
  } catch (error) {
    console.error('Error fetching data:', error)
    message.value = 'Failed to load message from backend'
  }
}

onMounted(() => {
  fetchData()
})


</script>
