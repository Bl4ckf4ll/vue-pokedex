<template>
    <div class="container px-10 my-10 mx-auto">
        <div v-if="pokemons.length > 0">
            <div class="flex flex-wrap">
                <div v-for="pokemon in pokemons" v-bind:key="pokemon.id" class="w-1/4 p-2">
                    <Pokemon :url="pokemon.url" :openModal="openModal">
                        <h3 slot="name">{{ pokemon.name }}</h3>
                    </Pokemon>
                </div>
            </div>
            <div class="p-2 text-center">
                <button v-if="next" class="bg-blue px-5 py-3 text-white rounded shadow" @click="loadMore">Load More</button>
            </div>
        </div>
        <div v-else>
            <h1 class="text-grey">No pokemons to show</h1>
        </div>
        <Modal id="pokemonDetail" :class="{ hidden: hideModal }" :pokemon="pokemon"></Modal>
    </div>
</template>

<script>
  import Pokemon from './Pokemon';
  import axios from 'axios';
  import Modal from "./Modal";
  import Bus from '../Bus';

  export default {
    name: 'Content',
    components: {
      Modal,
      Pokemon
    },
    props: {
      title: String,
    },
    data() {
      return {
        pokemons: [],
        hideModal: true,
        pokemon: null,
        next: null,
      };
    },
    mounted() {
      axios
        .get('https://pokeapi.co/api/v2/pokemon/')
        .then(({data}) => {
          this.pokemons = data.results;
          this.next = data.next;
        });

      Bus.$on('openModal', (data) => {
        this.openModal(data);
      });

      Bus.$on('hideModal', () => {
        this.closeModal();
      })
    },
    methods: {
      openModal(pokemon) {
        this.hideModal = false;
        this.pokemon = pokemon;
      },
      closeModal() {
        this.hideModal = true;
      },
      loadMore() {
        axios
          .get(this.next)
          .then(({data}) => {
            this.pokemons = [...this.pokemons, ...data.results];
            this.next = data.next;
          });
      }
    }
  }
</script>
