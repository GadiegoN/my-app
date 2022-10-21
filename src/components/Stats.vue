<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <v-row>
    <v-col
      cols="12"
      md="2"
      v-for="(stat, index) in pokemon.stats"
      :key="stat.stat.name"
    >
      <v-chip
        :color="color[index]"
        style="width: 100%"
        class="d-flex justify-center text-center white--text"
      >
        {{ transform_name(stat.stat.name) }} {{ stat.base_stat }}
      </v-chip>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      color: [
        "blue",
        "red",
        "orange",
        "red darken-3",
        "orange darken-3",
        "green",
      ],
    };
  },
  props: {
    pokemon: Object,
  },
  methods: {
    transform_name(name) {
      if (name.includes("-")) {
        let parts = name.split("-");
        return `${parts[0].charAt(0).toUpperCase()} ${parts[1]
          .charAt(0)
          .toUpperCase()}${parts[1].slice(1)}`;
      }

      return name.charAt(0).toUpperCase() + name.slice(1);
    },
  },
};
</script>