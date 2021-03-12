<template>
  <v-app>
    <div class="background grey-text">
      <NavBar
        :filterOptions="this.filterOptions"
        :voiceNames="voiceNames"
        :sortOptions="sortOptions"
        @filterInput="search"
        @orderItems="orderItems"
        @selectRandom="selectRandom"
        class="marginWidth"
      />
      <v-main class="pb-12 mx-4">
        <VoiceContainer
          :randomVoice="this.randomVoice"
          :voices="this.filteredVoices"
          class="marginWidth"
        />
      </v-main>
      <Footer />
    </div>
  </v-app>
</template>

<script>
import VoiceContainer from "./components/VoiceContainer";
import NavBar from "./components/NavBar";
import Footer from "./components/Footer";
import voicesFile from "./voices";

export default {
  name: "App",

  components: {
    VoiceContainer,
    NavBar,
    Footer,
  },

  data: () => ({
    randomVoice: {},
    filteredVoices: [],
    voices: voicesFile,
  }),
  computed: {
    filterOptions() {
      const tags = this.voices.flatMap((item) => item.tags);
      [...new Set(tags)];
      tags.unshift("View All");
      return tags;
    },
    voiceNames() {
      const voices = this.voices.map((voice) => voice.name);
      voices.unshift("View All");
      return voices;
    },
    sortOptions() {
      return ["A-Z", "Z-A"];
    },
  },
  methods: {
    search(e, item = "name") {
      console.log(e, item);
      if (e === "View All") {
        return (this.filteredVoices = this.voices);
      }
      const filteredVoices = this.voices.filter((voice) => {
        return item == "name"
          ? voice[item].toLowerCase().includes(e.toLowerCase())
          : voice[item].includes(e);
      });
      this.filteredVoices = filteredVoices;
    },
    orderItems(e) {
      const sortedArray = this.filteredVoices.sort(function(a, b) {
        var nameA = a.name.toUpperCase();
        var nameB = b.name.toUpperCase();
        if (nameA < nameB) {
          return -1;
        }
        if (nameA > nameB) {
          return 1;
        }
        return 0;
      });
      return e === "A-Z" ? sortedArray : sortedArray.reverse();
    },
    selectRandom() {
      const random = this.voices[
        Math.floor(Math.random() * this.voices.length)
      ];
      this.filteredVoices = this.voices;
      return (this.randomVoice = random);
    },
  },
  mounted() {
    this.filteredVoices = this.voices;
  },
};
</script>
<style>
.background {
  background-color: #1b1b1b;
  height: 100%;
}
.grey-text {
  color: #d2d2d2;
}
.greyBackground {
  background-color: #d2d2d2;
}
.marginWidth {
  max-width: 1246px;
  margin: auto;
}
</style>
