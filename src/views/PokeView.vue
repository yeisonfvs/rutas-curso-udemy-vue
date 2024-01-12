<script setup>
import axios from 'axios';
import { ref } from 'vue';
import { useRoute, useRouter } from 'vue-router';

const route = useRoute();
const router = useRouter();

const poke = ref({});

const back = () => {
  router.push('/pokemons');
};

const getData = async () => {
  try {
    const { data } = await axios.get(
      `https://pokeapi.co/api/v2/pokemon/${route.params.name}`
    );
    console.log(data);
    poke.value = data;
  } catch (error) {
    console.log(error);
    poke.value = null;
  }
};

getData();
</script>

<template>
  <div v-if="poke">
    <img :src="poke.sprites?.front_default" />
    <img :src="poke.sprites?.front_shiny" />
    <img :src="poke.sprites?.back_shiny" />
    <h1>Poke name: {{ $route.params.name }}</h1>
    <h2>id: {{ poke.id }}</h2>
  </div>

  <h1 v-else>No existe el pokemon</h1>

  <button class="btn btn-outline-success" @click="back">volver</button>
</template>

<style>
img {
  width: 200px;
}
</style>
