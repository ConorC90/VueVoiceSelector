<template>
  <div class="mb-10">
    <v-app-bar absolute color="deep-purple accent-4" dark>
      <v-text-field label="Search" placeholder="Voices" filled rounded dense>
        <template v-slot:prepend-inner>
          <img src="../assets/search.png" />
        </template>
      </v-text-field>
      <v-toolbar-title>Voice Mod</v-toolbar-title>
      <v-spacer></v-spacer>

      <img src="../assets/order.png" alt="You fucked up boo" />

      <img src="../assets/button-random.svg" alt="You fucked up boo" />

      <img src="../assets/filter.png" alt="You fucked up boo" />
    </v-app-bar>
  </div>
</template>
<script>
export default {
  components: {},

  data: () => ({
    icons: {
      serachIcon: "",
      randomIcon: "",
      orderIcon: "",
      filterIcon: "",
    },
  }),
};
</script>
<style scoped></style>
