<script setup>
import { RouterLink } from 'vue-router';
import { useGetData } from '@/composables/getData';

const { getData, data, loading, error } = useGetData();

// <----Esto se remplaza por el composable---->
//
// const getData = async () => {
//   try {
//     const { data } = await axios.get('https://pokeapi.co/api/v2/pokemon');
//     pokemons.value = data.results;
//     console.log(data.results);
//   } catch (error) {
//     console.log(error);
//   }
// };

getData('https://pokeapi.co/api/v2/pokemon');
</script>

<template>
  <h1>pokemons</h1>
  <p v-if="loading">Cargando informacion...</p>
  <div class="alert alert-danger" v-if="error">{{ error }}</div>
  <div v-if="data">
    <ul class="list-group mb-2">
      <li class="list-group-item" v-for="poke in data.results">
        <router-link :to="`/pokemons/${poke.name}`">
          {{ poke.name }}
        </router-link>
      </li>
    </ul>
    <button
      class="btn btn-success me-2"
      @click="getData(data.previous)"
      :disabled="!data.previous"
    >
      Previus
    </button>
    <button
      class="btn btn-primary"
      @click="getData(data.next)"
      :disabled="!data.next"
    >
      Next
    </button>
  </div>
</template>
