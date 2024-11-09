<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'

const projects = ref([])

onMounted(() => {
  axios.get(`${import.meta.env.VITE_API_BASE_URL}/projects`)
    .then(response => {
      projects.value = response.data
    })
    .catch(error => {
      console.error("Errore nel recupero dei progetti:", error)
    })
})
</script>


<template>
  <header>
    <h1>Progetti</h1>
  </header>

  <main>
    <div v-for="project in projects" :key="project.id">
      <ProjectCard :project="project" />
    </div>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>