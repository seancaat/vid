<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
import Footer from "@/components/Video.vue";

export default {
  data() {
    return {
      showAbout: false,
    }
  },
  components: {
    Footer
  },
  methods: {
    toggleAbout() {
      this.showAbout = !this.showAbout;
    }
  }
}
</script>

<style lang="scss">
body {
  font-family: sans-serif;
}

</style>
