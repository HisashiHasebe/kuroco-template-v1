<template>
  <div class="l-container--wrap">
    <nav class="l-breadcrumb is-pc">
      <div class="l-container--middle">
        <ul>
          <li><nuxt-link to="/">トップ</nuxt-link></li>
          <li><nuxt-link to="/news/">ニュース</nuxt-link></li>
          <li>{{ response.details.subject }}</li>
        </ul>
      </div>
    </nav>

    <div class="l-container--middle l-container--contents">

      <div class="l-container--main">
        <article class="c-article p-newsDetail">
          <div class="p-newsDetail__head">
            <time class="p-newsDetail__head__date" :datetime=response.details.ymd>{{ response.details.ymd }}</time>
            <div class="p-newsDetail__head__label">{{response.details.contents_type_nm}}</div>
            <h1 class="c-heading--lv1 p-newsDetail__head__heading">{{ response.details.subject }}</h1>
          </div>

          <div v-html="response.details.contents"></div>

          <div class="p-newsDetail__foot">
            <nuxt-link to="/news/"
              class="c-button--return icon-arrow-left">ニュース一覧へ戻る</nuxt-link>
          </div>
        </article>
      </div>

      <div class="l-container--side">
        <nav class="l-side">
          <h2 class="c-heading--lv2">アーカイブ</h2>
          <ul class="c-list--link">
            <li v-for="(n,i) in reverseItems" :key=i>
              <nuxt-link :to="`/news/?filter=${n.Filter}`">
                <i class="c-link__icon c-list__icon -front fas fa-caret-right"></i>{{n.Year}}年{{n.Month}}月 ({{ n.Count }})</nuxt-link>
            </li>
          </ul>
        </nav>
      </div>

    </div>

  </div>
</template>

<script>
export default {
  async asyncData({ $axios, params }) {
    return {
      response: await $axios.$get(`/rcms-api/1/news/details/${params.slug}`),
      master: await $axios.$get('/rcms-api/1/master'),
    };
  },
  computed: {
    reverseItems() {
      return this.master.list.slice().reverse();
    },
  },
};
</script>
