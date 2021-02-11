<template>
  <div
    class="memory-card"
    :data-framework="card.name"
    @click="flipCard(index)"
    :class="{ flip: card.flipped, 'disable-card': card.disabled }"
  >
    <img
      class="front-face"
      :src="require(`../assets/img/${card.name}.svg`)"
      :alt="card.name"
    />
    <img class="back-face" src="../assets/img/js-badge.svg" alt="JS Badge" />
  </div>
</template>

<script>
export default {
  props: {
    card: Object,
    index: Number,
  },
  methods: {
    flipCard(index) {
      this.$emit("flipCard", index);
    },
  },
};
</script>

<style></style>
