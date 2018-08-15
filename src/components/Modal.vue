<template>
    <div class="modal-mask items-center justify-center h-screen w-screen fixed pin-t pin-l overflow-auto" @click="hideModal">
        <div v-if="pokemon" class="mt-20 mb-20 mx-auto bg-grey-lighter w-1/2 p-10">
            <h1 class="mb-2 capitalize">{{ pokemon.name }}</h1>
            <small v-for="type in pokemon.types" v-bind:key="type.slot"
                   :class="[ type.type.name, 'py-1', 'px-2', 'rounded', 'mr-2', 'text-white' ]">
                {{ type.type.name }}
            </small>
            <!-- details -->
            <h2 class="my-2">Characteristics</h2>
            <div class="flex justify-around p-10">
                <h4>Weight: {{ pokemon.weight }}</h4>
                <h4>Height: {{ pokemon.height }}</h4>
            </div>
            <!-- pictures -->
            <div class="flex">
                <div class="w-1/2 p-10 bg-black text-white text-center">
                    <h3>Normal</h3>
                    <div class="flex">
                        <div class="w-1/2 text-center">
                            <img :src="pokemon.sprites.front_default" alt="front default">
                            <h4>Front</h4>
                        </div>
                        <div class="w-1/2 text-center">
                            <img :src="pokemon.sprites.back_default" alt="front default">
                            <h4>Back</h4>
                        </div>
                    </div>
                </div>
                <div class="w-1/2 p-10 text-center text-white bg-grey">
                    <h3>Shiny</h3>
                    <div class="flex">
                        <div class="w-1/2 text-center">
                            <img :src="pokemon.sprites.front_shiny" alt="front default">
                            <h4>Front</h4>
                        </div>
                        <div class="w-1/2">
                            <img :src="pokemon.sprites.back_shiny" alt="front default">
                            <h4>Back</h4>
                        </div>
                    </div>
                </div>
            </div>
            <!-- Stats -->
            <h2 class="mx-5 mt-10">Stats</h2>
            <div class="flex flex-wrap">
                <div class="w-1/3 p-10">
                    <h2>{{ speed.base_stat }}</h2>
                    <small>Speed</small>
                </div>
                <div class="w-1/3 p-10">
                    <h2>{{ specialDefense.base_stat }}</h2>
                    <small>Special Defense</small>
                </div>
                <div class="w-1/3 p-10">
                    <h2>{{ specialAttack.base_stat }}</h2>
                    <small>Special Attack</small>
                </div>
                <div class="w-1/3 p-10">
                    <h2>{{ defense.base_stat }}</h2>
                    <small>Defense</small>
                </div>
                <div class="w-1/3 p-10">
                    <h2>{{ attack.base_stat }}</h2>
                    <small>Attack</small>
                </div>
                <div class="w-1/3 p-10">
                    <h2>{{ hp.base_stat }}</h2>
                    <small>Hit Points</small>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
  import Bus from '../Bus';

  export default {
    name: 'Modal',
    props: {
      pokemon: Object,
    },
    methods: {
      hideModal() {
        Bus.$emit('hideModal');
      }
    },
    computed: {
      speed() {
        return this.pokemon.stats.find(stat => stat.stat.name === 'speed');
      },
      specialDefense() {
        return this.pokemon.stats.find(stat => stat.stat.name === 'special-defense');
      },
      specialAttack() {
        return this.pokemon.stats.find(stat => stat.stat.name === 'special-attack');
      },
      defense() {
        return this.pokemon.stats.find(stat => stat.stat.name === 'defense');
      },
      attack() {
        return this.pokemon.stats.find(stat => stat.stat.name === 'attack');
      },
      hp() {
        return this.pokemon.stats.find(stat => stat.stat.name === 'hp');
      },
    }
  }
</script>

<style scoped>
    .modal-mask {
        background-color: rgba(0, 0, 0, 0.2);
    }

    .pokemon {
        cursor: pointer;
        transition: all .5s;
    }

    .pokemon:hover {
        box-shadow: 0 2px 10px 0 rgba(0, 0, 0, .4)
    }

    .normal {
        background-color: #A8A878;
        border: 1px solid #6D6D4E;
    }

    .fire {
        background-color: #F08030;
        border: 1px solid #9C531F;
    }

    .water {
        background-color: #6890F0;
        border: 1px solid #445E9C;
    }

    .electric {
        background-color: #F8D030;
        border: 1px solid #A1871F;
    }

    .grass {
        background-color: #78C850;
        border: 1px solid #4E8234;
    }

    .ice {
        background-color: #98D8D8;
        border: 1px solid #638D8D;
    }

    .ground {
        background-color: #E0C068;
        border: 1px solid #927D44;
    }

    .flying {
        background-color: #A890F0;
        border: 1px solid #6D5E9C;
    }

    .ghost {
        background-color: #705898;
        border: 1px solid #493963;
    }

    .rock {
        background-color: #B8A038;
        border: 1px solid #786824;
    }

    .fighting {
        background-color: #C03028;
        border: 1px solid #7D1F1A;
    }

    .poison {
        background-color: #A040A0;
        border: 1px solid #682A68;
    }

    .psychic {
        background-color: #F85888;
        border: 1px solid #A13959;
    }

    .bug {
        background-color: #A8B820;
        border: 1px solid #6D7815;
    }

    .dark {
        background-color: #705848;
        border: 1px solid #49392F;
    }

    .steel {
        background-color: #B8B8D0;
        border: 1px solid #787887;
    }

    .dragon {
        background-color: #7038F8;
        border: 1px solid #4924A1;
    }
</style>
