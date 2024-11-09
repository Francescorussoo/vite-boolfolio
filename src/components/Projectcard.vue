<template>
    <div class="project-card">
      <h2>{{ project.title }}</h2>
      <p>{{ project.description }}</p>
      <img v-if="project.image" :src="`http://localhost:8000/storage/${project.image}`" alt="Immagine"/>
  
      <a :href="project.url" target="_blank" class="project-link">Visita</a>
    </div>
  </template>
  
  <script setup>
import { defineProps } from 'vue';

const props = defineProps({
  project: Object
});
</script>
  
  <style scoped>
  .project-card {
    border: 1px solid #ddd;
    padding: 1rem;
    border-radius: 8px;
    margin-bottom: 1rem;
  }
  .project-link {
    color: #42b883;
    text-decoration: none;
  }
  </style>
  