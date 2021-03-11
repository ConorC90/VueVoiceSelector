<template>
  <v-row class="mb-14" absolute dark>
    <v-col cols="4">
      <v-autocomplete
        :items="voiceNames"
        v-model="searchTerm"
        label="Search"
        placeholder="Voices"
        filled
        autofocus
        any
        rounded
        dense
        @change="$emit('searchInput', $event)"
      >
        <template v-slot:prepend-inner>
          <img src="../assets/search.png" />
        </template>
      </v-autocomplete>
    </v-col>
    <v-spacer></v-spacer>
    <v-col cols="2">
      <v-select :items="filterOptions" filled label="Filled style">
        <template v-slot:prepend>
          <img src="../assets/filter.png" />
        </template>
      </v-select>
    </v-col>
    <v-col cols="2">
      <v-select :items="[]" filled label="Filled style">
        <template v-slot:prepend>
          <img src="../assets/order.png" />
        </template>
      </v-select>
    </v-col>
    <v-col cols="1">
      <img src="../assets/button-random.svg" alt="You fucked up boo"
    /></v-col>
  </v-row>
</template>
<script>
export default {
  props: {
    filterOptions: {
      type: Array,
      required: false,
    },
    voiceNames: {
      type: Array,
      required: false,
    },
  },
  components: {},

  data: () => ({
    searchTerm: "",
  }),
};
</script>
<style scoped></style>
