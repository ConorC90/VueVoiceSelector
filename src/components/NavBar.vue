<template>
  <v-container>
    <v-row class="mb-14" absolute dark>
      <v-col cols="12" lg="4" md="4" sm="6">
        <v-autocomplete
          @change="$emit('filterInput', $event, 'name')"
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
        >
          <template v-slot:prepend-inner>
            <img src="../assets/search.png" />
          </template>
        </v-autocomplete>
      </v-col>
      <v-spacer></v-spacer>
      <v-col cols="12" lg="2" md="3" sm="6">
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
      <v-col cols="10" lg="2" md="3" sm="6">
        <v-select
          @change="$emit('orderItems', $event)"
          :items="sortOptions"
          filled
          dark
          label="Order Voices"
        >
          <template v-slot:prepend>
            <img src="../assets/order.png" />
          </template>
        </v-select>
      </v-col>
      <v-col cols="2" lg="1" md="1" sm="2" xs="12">
        <v-tooltip bottom>
          <template v-slot:activator="{ on, attrs }">
            <span v-bind="attrs" v-on="on"
              ><img
                @click="$emit('selectRandom')"
                src="../assets/button-random.svg"
                alt="You fucked up boo"
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
  }),
};
</script>
