<template>
  <v-app>
    <div v-if="loading" id="loading">
      <v-progress-circular indeterminate />
    </div>
    <v-content>
      <nuxt />
    </v-content>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    loading: false,
  }),
  created() {
    this.$nuxt.$on("toggleLoading", (loading) => {
      this.loading = loading;
    });
  },
};
</script>

<style lang="scss">
#loading {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100vh;
  z-index: 9999;
  position: fixed;
  background-color: rgba(#000, 0.5);
}
</style>