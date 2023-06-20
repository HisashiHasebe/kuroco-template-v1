<template>
  <section class="l-container--middle l-container--contents t-article-list">
    <ul v-if="cards.length" class="c-topics__card__list">
      <UiCard v-for="card in cards" :key="card.href" v-bind="card" />
    </ul>
    <slot />
  </section>
</template>

<script>
export default {
  props: {
    cards: {
      type: Array,
      required: true,
    },
  },
};
</script>
