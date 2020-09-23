<template>
  <v-container class="text-center my-12">
    <v-btn color="secondary" @click="submit">Submit</v-btn>
  </v-container>
</template>

<script>
export default {
  methods: {
    submit() {
      this.toggleLoading(true);
      setTimeout(() => {
        this.toggleLoading(false);
      }, 3000);
    },
    toggleLoading(loading) {
      this.$nuxt.$emit("toggleLoading", loading);
    },
  },
};
</script>