<template lang="">
    <div class="card">
    <div class="img"><img :src="pelicula.portada" :alt="pelicula.titulo" height="218px" /></div>
    <h1>{{ pelicula.titulo }} <br/>({{ pelicula.anio }}) </h1>
    <p><strong>Director:</strong> {{ pelicula.director }}</p>
      <p><strong>Géneros:</strong> {{ pelicula.generos.join(', ') }}</p>
      <p><strong>Likes:</strong> {{ pelicula.likes }}</p>
      <button @click="incrementarLike">❤️ Like</button> 
    </div>
</template>




<script setup>
import { ref } from 'vue';
import { peliculas } from '../Interfaces/Pelicula';


const props = defineProps({
        pelicula: Object
})
const emit = defineEmits(['like']);

const localLikes = ref(props.pelicula.likes);
const incrementarLike = () => {
  localLikes.value++;
  emit('like', { id: props.pelicula.id, likes: localLikes.value });
};

</script>

<style scoped>
    .card {
        border: 1px solid #ccc;
  padding: 1rem;
  margin: 1rem;
  border-radius: 8px;
  width: 200px;
  height: 40rem;
  text-align: center;
  display: grid;
    justify-items: center;
    align-content: stretch;
    align-items: end;
    }

    h1{
        font-size: 1.5rem;
        color: #443853;
    }

    p{
        line-height: normal;
        margin-top: 0;
        margin-bottom: 0;
    }
</style>