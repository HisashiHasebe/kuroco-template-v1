<template>
  <div>
    <UiMainSlider v-if="mainVisual" v-bind="mainVisual" />
    <NewsList v-if="news" v-bind="news" />

    <UiCardContainer v-if="cards && cards.length" :cards="cards">
      <div class="u-flex-horizon-center">
        <NuxtLink class="c-button icon-arrow-right" to="/service/">
          一覧へ
        </NuxtLink>
      </div>
    </UiCardContainer>
    <KurocoChat />
  </div>
</template>

<script>
// 画像をKurocoFilesを使わずにNuxtのassetsから配信することも可能です。
import dummyImage from '@/assets/image/600x400.png';

export default {
  data() {
    return {
      cards: [
        {
          href: '/service/#service-01',
          imageUrl: dummyImage,
          text: 'テキストが入ります。テキストが入ります。',
        },
        {
          href: '/service/#service-02',
          imageUrl: dummyImage,
          text: 'テキストが入ります。テキストが入ります。',
        },
        {
          href: '/service/#service-03',
          imageUrl: dummyImage,
          text: 'テキストが入ります。テキストが入ります。',
        },
      ],
      news: null,
      mainVisual: null,
    };
  },
  async asyncData({ $axios }) {
    return {
      news: await $axios.$get('/rcms-api/1/news/list', {
        params: { cnt: 3 },
      }),
      mainVisual: await $axios.$get('/rcms-api/1/main_visual'),
    };
  },
};
</script>

<style>
li.flex-active-slide {
  display: block !important;
}

@media all and (max-width: 768px) {
  .sp {
    display: block;
  }

  .pc {
    display: none;
  }
}

@media all and (min-width: 769px) {
  .sp {
    display: none;
  }

  .pc {
    display: block;
  }
}
</style>
