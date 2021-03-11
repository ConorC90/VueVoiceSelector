<template>
  <div class="mt-6">
    <v-row class="align-center">
      <h2 class="mr-2">Favourite Voices</h2>
      <v-divider class="greyCustom"></v-divider>
    </v-row>
    <v-row class="text-center">
      <v-col
        v-for="voice in favourites"
        :key="voice.id"
        @click="selectVoice(voice)"
      >
        <ItemImage
          @clickedFavourite="favouriteClick(voice)"
          :item="voice"
          :isFavourite="isFavourite(voice)"
          :isActive="isActive(voice)"
        />
      </v-col>
    </v-row>
    <v-row class="align-center">
      <h2 class="mr-2">Pro Voices</h2>
      <v-divider class="active"></v-divider>
    </v-row>
    <v-row class="text-center">
      <v-col
        v-for="voice in voices"
        :key="voice.id"
        @click="selectVoice(voice)"
      >
        <ItemImage
          @clickedFavourite="favouriteClick(voice)"
          :item="voice"
          :isFavourite="isFavourite(voice)"
          :isActive="isActive(voice)"
        />
      </v-col>
    </v-row>
  </div>
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
  },
  name: "HelloWorld",
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
      const itemIndex = this.favourites.indexOf(item);
      itemIndex === -1
        ? this.favourites.push(item)
        : this.favourites.splice(itemIndex, 1);
    },
    selectVoice(voice) {
      this.selectedVoice = voice;
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
<style scoped></style>
