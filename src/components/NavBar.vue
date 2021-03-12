<template>
  <v-container>
    <v-row class="mb-14 align-center" absolute dark>
      <v-col cols="12" lg="4" md="4" sm="6">
        <v-autocomplete
          @change="input('filterInput', $event, 'name')"
          :items="voiceNames"
          v-model="searchTerm"
          label="Search"
          placeholder="Type something"
          dark
          filled
          autofocus
          any
          rounded
          dense
        >
          <template v-slot:prepend-inner>
            <img src="../assets/search.png" alt="Search Voices" />
          </template>
        </v-autocomplete>
      </v-col>
      <v-spacer></v-spacer>
      <v-col cols="12" lg="3" md="3" sm="6">
        <v-select
          @change="input('filterInput', $event, 'tags')"
          :items="filterOptions"
          v-model="filterTerm"
          filled
          dark
          label="Filter Catogary"
        >
          <template v-slot:prepend>
            <img src="../assets/filter.png" alt="Filter Voices" />
          </template>
        </v-select>
      </v-col>
      <v-col cols="10" lg="2" md="3" sm="6">
        <v-select
          @change="$emit('orderItems', $event)"
          :items="sortOptions"
          filled
          dark
          label="Order Voices"
        >
          <template v-slot:prepend>
            <img src="../assets/order.png" alt="Order Voices" />
          </template>
        </v-select>
      </v-col>
      <v-col cols="2" lg="1" md="1" sm="2" xs="12">
        <v-tooltip bottom>
          <template v-slot:activator="{ on, attrs }">
            <span v-bind="attrs" v-on="on"
              ><img
                @click="selectedRandom()"
                src="../assets/button-random.svg"
                alt="Select Random Voice"
            /></span>
          </template>
          <span>Select a random voice</span>
        </v-tooltip>
      </v-col>
    </v-row>
  </v-container>
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
    sortOptions: {
      type: Array,
      required: false,
    },
  },

  data: () => ({
    searchTerm: "",
    filterTerm: "",
  }),
  methods: {
    input(filterInput, e, type) {
      this.$emit(filterInput, e, type);
      type === "name" ? (this.filterTerm = "") : (this.searchTerm = "");
    },
    selectedRandom() {
      this.filterTerm = "";
      this.searchTerm = "";
      this.$emit("selectRandom");
    },
  },
};
</script>
