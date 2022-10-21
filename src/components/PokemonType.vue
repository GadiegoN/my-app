<template>
  <v-chip color="blue" class="mr-2 white--text"> {{ name }}</v-chip>
</template>

<script>
export default {
  props: {
    type: String,
  },
  computed: {
    name() {
      return this.type;
    },
  },
};
</script>

<style lang="scss" scoped></style>
