<template>
  <div class="home">
    <div v-for="(pokemon, i) in pokemons" :key="i"> 
      <p>{{ pokemon.name }}</p>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, ref } from 'vue';
import HelloWorld from '@/components/HelloWorld.vue'; // @ is an alias to /src


import api from "@/client/pokemon";

export default defineComponent({
  name: 'HomeView',
  components: {
    HelloWorld,
  },
  setup(){
    const pokemons = ref([])

    const fetchPokemons = () => api.get("/pokemon?limit=20").then((response) => pokemons.value = response.data.results)

    onMounted(fetchPokemons);

    return {pokemons}
  }
});
</script>
