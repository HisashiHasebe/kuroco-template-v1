<template>
  <div>
    <Header />

    <Nuxt />

    <Footer />
  </div>
</template>

<script>
export default {
  data() {
    return {
      Drawer: false,
    };
  },
  computed: {
    userName() {
      return this.$auth.user;
    },
    userStatus() {
      if ('105' in this.$auth.user.group_ids) {
        return this.$auth.user.group_ids['105'];
      } else {
        return this.$auth.user.group_ids['104'];
      }
    },
  },
};
</script>
