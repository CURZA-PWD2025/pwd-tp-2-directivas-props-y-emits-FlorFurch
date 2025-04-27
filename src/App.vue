<template>
  <div class="container">
    <CardComponent
      v-for="pelicula in peliculas"
      :key="pelicula.id"
      :pelicula="pelicula"
      @toggle-like="handleToggleLike"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import { peliculas as peliculasData } from './resources/peliculas';
import type { Pelicula } from './Interfaces/Pelicula';
import CardComponent from './components/CardComponent.vue';

export default defineComponent({
  name: 'App',
  components: {
    CardComponent,
  },
  setup() {
    const peliculas = ref<Pelicula[]>(peliculasData);

    const handleToggleLike = (data: { id: number; liked: boolean }) => {
      const pelicula = peliculas.value.find(p => p.id === data.id);
      if (pelicula) {
        if (data.liked) {
          pelicula.likes++;
        } else {
          pelicula.likes--;
        }
      }
    };

    return {
      peliculas,
      handleToggleLike,
    };
  },
});
</script>

<style scoped>
.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
</style>