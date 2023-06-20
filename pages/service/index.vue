<template>
  <PlainContent v-bind="details" />
</template>

<script>
export default {
  async asyncData({ $axios, params }) {
    const response = await $axios.$get(`/rcms-api/1/content/details/service`);
    return {
      details: response.details,
    };
  },
};
</script>
