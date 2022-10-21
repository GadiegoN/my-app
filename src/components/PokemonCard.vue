<template>
  <v-card 
    @click="show_pokemon(get_id(pokemon))"
    :flat="flat"
    color="#a7a6a6"
    class="card"
  >
    <v-container>
      <v-row class="mx-0 d-flex justify-center">
        <img
          :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${get_id(
            pokemon
          )}.png`"
          :alt="pokemon.name"
          width="80%"
        />
        <h2 class="text-center">{{ get_name(pokemon) }}</h2>
      </v-row>
      <v-row class="mx-0 d-flex justify-center">
        <span>{{ get_id(pokemon) }}</span>
      </v-row>
    </v-container>
  </v-card>
</template>

<script>
export default {
  props: {
    pokemon: Object,
    flat: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    get_id(pokemon) {
      return Number(pokemon.url.split("/")[6]);
    },
    get_name(pokemon) {
      return pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1);
    },
    show_pokemon(id) {
      this.$emit("clicked", id);
    },
  },
};
</script>

<style lang="scss" scoped>
  h2 {
    color: white;
  }
  .card:hover {
    scale: 1.1;
  }
</style>
