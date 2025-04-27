<template>
  <div class="card">
    <img v-if="pelicula.portada" :src="pelicula.portada" alt="Portada"/>
    <div v-else>
  Imagen de portada no encontrada
</div>
    <h2>{{ pelicula.titulo }}</h2>
    <p>{{ pelicula.generos.join(" / ") }}</p>
    <p>{{ pelicula.anio }}</p>
    <div>
      <button @click="toggleLike">
        {{ isLiked ? 'No me gusta' : 'Me gusta!' }}
      </button>
      
    </div>
    <div><span>❤️ {{ pelicula.likes }}</span></div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import type { PropType } from 'vue';
import type { Pelicula } from '../Interfaces/Pelicula';

export default defineComponent({
  name: 'CardComponent',
  props: {
    pelicula: {
      type: Object as PropType<Pelicula>,
      required: true,
    },
  },
  setup(props, { emit }) {
    const isLiked = ref(false);

    const toggleLike = () => {
      isLiked.value = !isLiked.value;
      emit('toggle-like', { id: props.pelicula.id, liked: isLiked.value });
    };

    return {
      isLiked,
      toggleLike,
    };
  },
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

    h1{
        font-size: 1.5rem;
        color: #443853;
    }

    p{
        line-height: normal;
        margin-top: 0;
        margin-bottom: 0;
    }

    div{
      padding: 2px;
    }


</style>