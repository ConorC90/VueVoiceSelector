<template>
  <v-col
    @mouseover="isHovering = true"
    @mouseleave="isHovering = false"
    class="container"
  >
    <div
      v-if="isHovering || this.isMobile"
      @click="clickedFavourite"
      class="overlay"
    >
      <img
        v-if="isFavourite"
        src="../assets/voice-favourite.svg"
        alt="favorited item"
      />
      <img
        v-if="!isFavourite"
        src="../assets/voice-favourite-off.svg"
        alt="unfavorited item"
      />
    </div>
    <div>
      <v-avatar
        size="120"
        class="grey-background"
        :class="{ 'active-background': isActive }"
        @click="clickedVoice"
      >
        <div>
          <img :src="require(`../assets/${item.icon}`)" alt="Voice Icon" />
        </div>
      </v-avatar>
      <div :class="{ 'active-text': isActive }">
        {{ item.name }}
      </div>
    </div>
  </v-col>
</template>

<script>
export default {
  data() {
    return {
      isHovering: undefined,
    };
  },
  props: {
    item: {
      type: Object,
      required: true,
    },
    isFavourite: {
      type: Boolean,
      required: true,
    },
    isActive: {
      type: Boolean,
      required: true,
    },
  },
  computed: {
    isMobile() {
      return window.innerWidth < 600;
    },
  },
  methods: {
    clickedFavourite() {
      this.$emit("clickedFavourite");
    },
    clickedVoice() {
      this.$emit("selectVoice");
    },
  },
};
</script>
<style scoped>
.grey-background {
  background-color: #d2d2d2;
}
.active-background {
  background: linear-gradient(#00c9ff, #00e5ff);
}
.active-text {
  color: #00d9ff;
}
.container {
  position: relative;
  width: 150px;
}
.overlay {
  width: 23px;
  height: 23px;
  background-color: #d2d2d2;
  border-radius: 50%;
  position: absolute;
  top: 15px;
  right: 20px;
  z-index: 2;
}
</style>
