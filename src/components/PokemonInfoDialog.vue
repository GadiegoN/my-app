<!-- eslint-disable vue/no-mutating-props -->
<template>
  <v-dialog v-model="show" width="800" dark >
    <v-toolbar
      dark
      color="dark"
    >
      <v-btn
        icon
        dark
        @click="show = false"
      >
        <v-icon>mdi-close</v-icon>
      </v-btn>
      <v-toolbar-title>{{ get_name(selected_pokemon) }}</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items>
        <v-btn
          dark
          text
          @click="show = false"
        >
          Favoritar
        </v-btn>
      </v-toolbar-items>
    </v-toolbar>
    <v-card v-if="selected_pokemon" class="px-4">
      <v-container>
        <v-row class="d-flex align-center">
          <v-col cols="12" md="4">
            <img
              :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${selected_pokemon.id}.png`"
              :alt="selected_pokemon.name"
              width="80%"
            />
          </v-col>
          <v-col cols="12" md="8">
            <PokemonType
              v-for="type in selected_pokemon.types"
              :key="type.slot"
              :type="type.type.name"
            />

            <v-divider class="my-4"> </v-divider>
            <v-chip label
              >Height {{ selected_pokemon.height * 2.54 }} cm</v-chip
            >
            <v-chip label class="ml-2"
              >Weight
              {{ (selected_pokemon.weight * 0.45359237).toFixed(0) }}
              kgs</v-chip
            >
          </v-col>
        </v-row>

        <v-divider class="my-4"></v-divider>

        <h2 class="mt-4">Caracteristicas</h2>

        <Stats class="mt-2" :pokemon="selected_pokemon" />

        <v-divider class="my-4"></v-divider>

        <h2>Evolução</h2>

        <EvolutionChain :pokemon="selected_pokemon" />
      </v-container>
    </v-card>
  </v-dialog>
</template>

<script>
import EvolutionChain from "./EvolutionChain.vue";
import Stats from "./Stats.vue";
import PokemonType from "./PokemonType.vue";

export default {
  components: {
    EvolutionChain,
    Stats,
    PokemonType,
  },
  props: {
    show: Boolean,
    selected_pokemon: Object,
  },
  methods: {
    get_name(pokemon) {
      return pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1);
    },
    transform_move_name(name) {
      let response = "";
      for (let part of name.split("-")) {
        response += part.charAt(0).toUpperCase() + part.slice(1) + " ";
      }
      return response;
    },
  },
  computed: {},
  watch: {
    show() {
      this.$emit("update:show", this.show);
    },
  },
};
</script>

<style lang="scss" scoped>

</style>
