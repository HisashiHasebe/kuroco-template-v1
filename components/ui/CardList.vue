<template>
  <div>
    <ul v-if="list.length" class="c-card-list c-card-list--col-3">
      <li v-for="card in list" :key="card.topics_id">
        <NuxtLink class="c-card" :to="`/ltd-news/detail/${card.topics_id}`">
          <div class="c-card__image">
            <span class="c-card__image__badge">
              {{ card.contents_type_nm }}
            </span>
            <img alt="dummy picture" :src="card.ext_1.url" />
          </div>
          <p class="c-card__heading">{{ card.subject }}</p>
        </NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    list: {
      type: Array,
      required: true,
    },
  },
};
</script>
