<template>
    <div class="container px-10 my-10 mx-auto">
        <div v-if="pokemons.length > 0">
            <div class="flex flex-wrap">
                <div v-for="pokemon in pokemons" v-bind:key="pokemon.id" class="w-1/4 p-2">
                    <Pokemon :url="pokemon.url">
                        <h3 slot="name">{{ pokemon.name }}</h3>
                    </Pokemon>
                </div>
            </div>
        </div>
        <div v-else>
            <h1 class="text-grey">No pokemons to show</h1>
        </div>
    </div>
</template>

<script>
  import Pokemon from './Pokemon';
  import axios from 'axios';

  export default {
    name: 'Content',
    components: {
      Pokemon
    },
    props: {
      title: String,
    },
    data () {
      return {
        pokemons: [],
      };
    },
    mounted () {
      axios
        .get('https://pokeapi.co/api/v2/pokemon/')
        .then(({ data }) => (this.pokemons = data.results));
    },
  }
</script>

<style scoped>

</style>