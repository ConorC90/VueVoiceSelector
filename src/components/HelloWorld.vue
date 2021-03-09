<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <h1>Main Container</h1>
        <h2>Selected= {{ selectedVoice }}</h2>
        <h2>Besties</h2>
        <ul>
          <li v-for="(voice, index) in favourites" :key="index">
            <ItemImage
              @clickedFavourite="favouriteClick(voice)"
              :item="voice"
              :isFavourite="isFavourite(voice)"
              :isActive="selectedVoice === voice"
            />
          </li>
        </ul>
        <h2>All</h2>
        <ul>
          <li
            v-for="voice in voices"
            :key="voice.id"
            @click="selectVoice(voice)"
          >
            <ItemImage
              @mouseover="isHovering = true"
              @mouseleave="isHovering = false"
              @clickedFavourite="favouriteClick(voice)"
              :item="voice"
              :isFavourite="isFavourite(voice)"
              :isActive="selectedVoice === voice"
            />
          </li>
        </ul>
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
  },
  name: "HelloWorld",
  data() {
    return {
      isHovering: "",
      favourites: [],
      selectedVoice: "",
    };
  },
  computed: {},
  methods: {
    favouriteClick(item) {
      console.log(item);
      const itemIndex = this.favourites.indexOf(item);
      itemIndex === -1
        ? this.favourites.push(item)
        : this.favourites.splice(itemIndex, 1);
    },
    selectVoice(voice) {
      this.selectedVoice = voice;
    },
    isFavourite(item) {
      console.log(this.favourites.includes(item));
      return this.favourites.includes(item);
    },
  },
};
</script>
<style scoped>
.active {
  background-color: pink;
}
</style>
