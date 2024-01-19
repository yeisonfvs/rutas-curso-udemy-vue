<script setup>
import { useFavoritosStore } from '@/store/favoritos';
import { RouterLink } from 'vue-router';
import { storeToRefs } from 'pinia';

const useFavoritos = useFavoritosStore();

const { favoritos } = storeToRefs(useFavoritos);
const { remove } = useFavoritos;
</script>

<template>
  <h1>Favoritos</h1>
  <p v-if="favoritos.length === 0">Sin favoritos</p>
  <ul class="list-group" v-else>
    <li class="list-group-item" v-for="poke in favoritos" :key="poke.id">
      <div class="mb-2">
        {{ poke.name }}
      </div>
      <div>
        <router-link
          class="btn btn-sm btn-success me-3"
          :to="`/pokemons/${poke.name}`"
        >
          Mayor info
        </router-link>

        <button class="btn btn-sm btn-danger" @click="remove(poke.id)">
          Eliminar
        </button>
      </div>
    </li>
  </ul>
</template>
