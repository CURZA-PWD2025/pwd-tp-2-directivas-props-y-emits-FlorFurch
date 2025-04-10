<template>
  <div class="card">
    <div class="img"><img :src="pelicula.portada" :alt="pelicula.titulo" height="218px" /></div>
    <h3>{{ pelicula.titulo }}<br/>({{ pelicula.anio }})</h3>
    <p><strong>Director:</strong> {{ pelicula.director }}</p>
    <p><strong>Géneros:</strong> {{ pelicula.generos.join(', ') }}</p>
    <p><strong>Likes:</strong> {{ likes }}</p>
    <button @click="incrementarLike">❤️ Like</button>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import type { PropType } from 'vue';

export default defineComponent({
  name: 'CardComponent',
  props: {
    pelicula: {
      type: Object as PropType<{
        id: number;
        titulo: string;
        generos: string[];
        anio: number;
        director: string;
        likes: number;
        portada: string;
      }>,
      required: true
    }
  },
  setup(props) {
    const likes = ref(props.pelicula.likes);

    const incrementarLike = () => {
      likes.value++;
    };

    return {
      likes,
      incrementarLike
    };
  }
});
</script>

<style scoped>
.card {
  border: 1px solid #ccc;
  padding: 1rem;
  margin: 1rem;
  border-radius: 8px;
  width: 200px;
  text-align: center;
  display: grid;
    justify-items: center;
    align-content: stretch;
    align-items: end;
}
.img{
  height: 250px;
}
button {
  background-color: #e74c3c;
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  margin-top: 0.5rem;
  border-radius: 4px;
  cursor: pointer;
}
button:hover {
  background-color: #c0392b;
}
</style>