<template lang="">
  <div class="container">

    <div v-for="(pelicula, index) in peliculas" :key="pelicula.id">
      <Card :pelicula="pelicula" @like="actualizarLikes" />
    </div>

  </div>
</template>

<script setup>
import { reactive } from 'vue';
import Card from './components/Card.vue';
import { peliculas as dataPeliculas } from './Interfaces/Pelicula';

const peliculas = reactive([...dataPeliculas]);
const actualizarLikes = ({ id, likes }) => {
  const pelicula = peliculas.find(p => p.id === id);
  if (pelicula) {
    pelicula.likes = likes;
  }
};
</script>

<style scoped>
.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
</style>