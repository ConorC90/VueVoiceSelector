<template>
  <v-container class="mx-10" fluid>
    <v-row class="mb-14" absolute dark>
      <v-col cols="4" lg="2" md="3" sm="12" xs="12">
        <v-autocomplete
          :items="voiceNames"
          v-model="searchTerm"
          label="Search"
          placeholder="Voices"
          dark
          filled
          autofocus
          any
          rounded
          dense
          @change="$emit('filterInput', $event, 'name')"
        >
          <template v-slot:prepend-inner>
            <img src="../assets/search.png" />
          </template>
        </v-autocomplete>
      </v-col>
      <v-spacer></v-spacer>
      <v-col cols="2">
        <v-select
          @change="$emit('filterInput', $event, 'tags')"
          :items="filterOptions"
          filled
          dark
          label="Filled style"
        >
          <template v-slot:prepend>
            <img src="../assets/filter.png" />
          </template>
        </v-select>
      </v-col>
      <v-col cols="2">
        <v-select
          :items="sortOptions"
          filled
          dark
          label="Order Voices"
          @change="$emit('orderItems', $event)"
        >
          <template v-slot:prepend>
            <img src="../assets/order.png" />
          </template>
        </v-select>
      </v-col>
      <v-col cols="1">
        <img
          @click="$emit('selectRandom')"
          src="../assets/button-random.svg"
          alt="You fucked up boo"
      /></v-col>
    </v-row>
    <v-row v-if="$vuetify.breakpoint.xsOnly">
      <h2>Helllooooooooooooooo</h2>
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
  }),
};
</script>
