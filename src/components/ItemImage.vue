<template>
  <v-col @mouseover="isHovering = true" @mouseleave="isHovering = false">
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
    <div>
      <v-avatar
        size="120"
        class="grey-background"
        :class="{ 'active-background': isActive }"
      >
        <div>
          <img
            :src="require(`../assets/${item.icon}`)"
            alt="You fucked up boo"
          />
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
  methods: {
    clickedFavourite() {
      this.$emit("clickedFavourite");
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
</style>
