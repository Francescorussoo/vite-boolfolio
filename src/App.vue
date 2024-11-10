<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import ProjectCard from './components/ProjectCard.vue';

const projects = ref([]);

onMounted(() => {
  axios.get(`${import.meta.env.VITE_API_BASE_URL}/projects`)
    .then(response => {
      projects.value = response.data;
    })
    .catch(error => {
      console.error("Errore nel recupero dei progetti:", error);
    });
});
</script>

<template>
  <header>
    <h1>Progetti</h1>
    <nav>
      <router-link to="/">Home</router-link>
      <router-link to="/projects">Progetti</router-link>
      <router-link to="/about">Chi Siamo</router-link>
    </nav>
  </header>

  <main>
    <router-view/>
    <section v-if="$route.name === 'projects'">
      <div v-for="project in projects" :key="project.id">
        <ProjectCard :project="project"/>
      </div>
    </section>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
  text-align: center;
  margin-bottom: 2rem;
}

nav {
  margin-bottom: 1rem;
}

nav a {
  margin: 0 1rem;
  text-decoration: none;
  color: #42b983;
}

nav a.router-link-active {
  font-weight: bold;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
}
</style>
