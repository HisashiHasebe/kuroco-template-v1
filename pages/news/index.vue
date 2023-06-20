<template>
  <div class="l-container--wrap">
    <nav class="l-breadcrumb is-pc">
      <div class="l-container--middle">
        <ul>
          <li><NuxtLink to="/">トップ</NuxtLink></li>
          <li>ニュース</li>
        </ul>
      </div>
    </nav>

    <div class="l-container--middle l-container--contents">
      <div class="l-container--main">
        <section class="p-news">
          <h1 class="c-heading--lv1">ニュース</h1>
          <ul class="c-topics__list p-news__list">
            <div v-if="newsResponse.pageInfo.totalCnt === 0">
              記事が存在しません
            </div>
            <template v-else>
              <li
                v-for="news in newsResponse.list"
                :key="news.topics_id"
                class="c-topics__item"
              >
                <time class="c-topics__date" :datetime="news.ymd">{{
                  news.ymd
                }}</time>
                <div class="c-topics__label">
                  {{ news.contents_type_nm }}
                </div>
                <div class="c-topics__title">
                  <NuxtLink :to="`/news/detail/${news.topics_id}`">{{
                    news.subject
                  }}</NuxtLink>
                </div>
              </li>
            </template>
          </ul>
        </section>
      </div>

      <div class="l-container--side">
        <nav class="l-side">
          <h2 class="c-heading--lv2">アーカイブ</h2>
          <ul class="c-list--link">
            <li v-for="archive in archives" :key="archive.count">
              <NuxtLink :to="`/news/?filter=${archive.Filter}`">
                <i
                  class="c-link__icon c-list__icon -front fas fa-caret-right"
                ></i
                >{{ archive.Year }}年{{ archive.Month }}月 ({{
                  archive.Count
                }})</NuxtLink
              >
            </li>
          </ul>
        </nav>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  watchQuery: ['filter'],
  async asyncData({ $axios, query }) {
    const archiveMaster = await $axios.$get('/rcms-api/1/master');
    return {
      newsResponse: await $axios.$get('/rcms-api/1/news/list', {
        params: { filter: query.filter },
      }),
      archives: archiveMaster.list.slice().reverse(),
    };
  },
};
</script>
