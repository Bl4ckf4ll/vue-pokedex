<template>
    <div class="pokemon shadow p-4">
        <img v-if="info" :src="info.sprites.front_default" width="100" class="block mx-auto my-5" alt="info">
        <div class="mb-2">
            <slot name="name"></slot>
            <small v-if="info">N° {{ paddedOrder }}</small>
        </div>
        <ul v-if="info" class="p-0">
            <li v-for="type in info.types" v-bind:key="type.slot" class="inline mr-2">
                <small :class="[ type.type.name, 'py-1', 'px-2', 'rounded', 'text-white' ]">{{ type.type.name }}</small>
            </li>
        </ul>
    </div>
</template>

<script>
  import axios from 'axios';

  export default {
    name: 'Pokemon',
    props: {
      url: String,
    },
    data() {
      return {
        info: null,
      }
    },
    mounted() {
      axios
        .get(this.url)
        .then(({data}) => (this.info = data));
    },
    computed: {
      paddedOrder() {
        const order = this.info.order.toString();
        return order.padStart(3, '0');
      }
    }
  }
</script>

<style scoped>
    .pokemon {
        transition: all .5s;
    }

    .pokemon:hover {
        box-shadow: 0 2px 10px 0 rgba(0,0,0,.4)
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