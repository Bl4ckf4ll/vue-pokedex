<template>
    <div class="pokemon shadow p-4" @click="openModal(pokemon)">
        <div class="h-32">
            <img v-if="pokemon" :src="pokemon.sprites.front_default" class="h-24 block mx-auto my-5" alt="info">
            <img v-else src="../assets/images/pokeball.png" class="h-24 block mx-auto my-5 loader" alt="pokeballs">
        </div>
        <div class="mb-2">
            <slot name="name"></slot>
            <small v-if="pokemon">N° {{ paddedOrder }}</small>
            <small v-else>Loading...</small>
        </div>
        <ul v-if="pokemon" class="p-0">
            <li v-for="type in pokemon.types" v-bind:key="type.slot" class="inline mr-2">
                <small :class="[ type.type.name, 'py-1', 'px-2', 'rounded', 'text-white' ]">
                    {{ type.type.name }}
                </small>
            </li>
        </ul>
        <ul v-else>
            <li class="inline mr-2">
                <small :class="[ 'py-1', 'px-2', 'rounded', 'text-white', 'bg-grey' ]">
                    Loading...
                </small>
            </li>
        </ul>
    </div>
</template>

<script>
  import axios from 'axios';
  import Bus from '../Bus';

  export default {
    name: 'Pokemon',
    props: {
      url: String,
    },
    data() {
      return {
        pokemon: null,
      }
    },
    mounted() {
      axios
        .get(this.url)
        .then(({data}) => (this.pokemon = data));
    },
    computed: {
      paddedOrder() {
        const order = this.pokemon.order.toString();
        return order.padStart(3, '0');
      }
    },
    methods: {
      openModal(data) {
        Bus.$emit('openModal', data);
      }
    }
  }
</script>

<style scoped>
    .pokemon {
        cursor: pointer;
        transition: all .5s;
    }

    .pokemon:hover {
        box-shadow: 0 2px 10px 0 rgba(0, 0, 0, .4)
    }

    .normal {
        background-color: #A8A878;
    }

    .fire {
        background-color: #F08030;
    }

    .water {
        background-color: #6890F0;
    }

    .electric {
        background-color: #F8D030;
    }

    .grass {
        background-color: #78C850;
    }

    .ice {
        background-color: #98D8D8;
    }

    .ground {
        background-color: #E0C068;
    }

    .flying {
        background-color: #A890F0;
    }

    .ghost {
        background-color: #705898;
    }

    .rock {
        background-color: #B8A038;
    }

    .fighting {
        background-color: #C03028;
    }

    .poison {
        background-color: #A040A0;
    }

    .psychic {
        background-color: #F85888;
    }

    .bug {
        background-color: #A8B820;
    }

    .dark {
        background-color: #705848;
    }

    .steel {
        background-color: #B8B8D0;
    }

    .dragon {
        background-color: #7038F8;
    }

    .fairy {
        background-color: #EE99AC;
    }

    .loader {
        animation: loader infinite linear 1s;
    }

    @keyframes loader {
        0% {
            transform: rotate(0deg);
        }
        100% {
            transform: rotate(360deg);
        }
    }
</style>