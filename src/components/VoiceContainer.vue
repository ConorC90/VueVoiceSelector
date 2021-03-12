<template>
  <v-container>
    <v-row class="align-center">
      <h2 class="mr-2">Favourite Voices</h2>
      <v-divider class="greyBackground"></v-divider>
    </v-row>
    <v-row class="text-center">
      <p v-if="this.favourites.length == 0">
        To add favourites you can hover over a voice icon and click on the
        heart.
      </p>
      <v-col
        v-for="voice in favourites"
        :key="voice.id"
        lg="2"
        md="3"
        sm="4"
        xs="6"
      >
        <ItemImage
          @selectVoice="setSelectVoice(voice)"
          @clickedFavourite="favouriteClick(voice)"
          :item="voice"
          :isFavourite="isFavourite(voice)"
          :isActive="isActive(voice)"
        />
      </v-col>
    </v-row>
    <v-row class="align-center">
      <h2 class="mr-2">Pro Voices</h2>
      <v-divider class="greyBackground"></v-divider>
    </v-row>
    <v-row class="text-center">
      <p v-if="this.voices.length === 0">
        No voices to display
      </p>
      <v-col
        v-for="voice in voices"
        :key="voice.id"
        lg="2"
        md="3"
        sm="4"
        xs="6"
      >
        <ItemImage
          @selectVoice="setSelectVoice(voice)"
          @clickedFavourite="favouriteClick(voice)"
          :item="voice"
          :isFavourite="isFavourite(voice)"
          :isActive="isActive(voice)"
        />
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import ItemImage from "./ItemImage";
export default {
  components: {
    ItemImage,
  },
  props: {
    voices: {
      type: Array,
      required: true,
    },
    randomVoice: {
      type: Object,
      required: false,
    },
  },
  data() {
    return {
      favourites: [],
      selectedVoice: "",
    };
  },
  computed: {
    favouritesItems() {
      const array = this.favourites.filter((item) =>
        this.voicescd.includes(item)
      );
      return array;
    },
  },
  methods: {
    favouriteClick(item) {
      const isAFavourite = this.favourites
        .map((item) => item.id)
        .indexOf(item.id);
      isAFavourite === -1
        ? this.favourites.push(item)
        : this.favourites.splice(isAFavourite, 1);
    },
    setSelectVoice(voice) {
      this.selectedVoice !== voice
        ? (this.selectedVoice = voice)
        : (this.selectedVoice = {});
    },
    isFavourite(item) {
      return this.favourites.map((item) => item.id).includes(item.id);
    },
    isActive(item) {
      return this.selectedVoice.id === item.id;
    },
  },
  watch: {
    favourites(newFavourites) {
      localStorage.favourites = JSON.stringify(newFavourites);
    },
    selectedVoice(newSelectedVoice) {
      localStorage.selectedVoice = JSON.stringify(newSelectedVoice);
    },
    randomVoice(newRandomVoice) {
      this.selectedVoice = newRandomVoice;
    },
  },
  mounted() {
    if (localStorage.favourites) {
      this.favourites = JSON.parse(localStorage.favourites);
    }
    if (localStorage.selectedVoice) {
      this.selectedVoice = JSON.parse(localStorage.selectedVoice);
      this.selectedVoice.id === JSON.parse(localStorage.selectedVoice).id;
    }
  },
};
</script>
