<template>
  <div @mouseover="isHovering = true" @mouseleave="isHovering = false">
    <div v-if="isHovering" @click="clickedFavourite">
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
    {{ item.name }}
    <img :src="require(`../assets/${item.icon}`)" alt="You fucked up boo" />
  </div>
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
  methods: {
    clickedFavourite() {
      this.$emit("clickedFavourite");
    },
  },
};
</script>
