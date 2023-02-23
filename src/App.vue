<script lang="ts">
import Header from "./components/Header.vue";
import Middle1 from "./components/Middle1.vue";
import Middle2 from "./components/Middle2.vue";
import Upload from "./components/Upload.vue";
import ProgressBar from "./components/ProgressBar.vue";
export default {
  components: {
    Header,
    Middle1,
    Middle2,
    Upload,
    ProgressBar,
  },
};
</script>
<template>
  <nav>
    <Header />
    <Middle1 />
    <Middle2 />
    <Upload />
    <ProgressBar />
    <!-- <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link> -->
  </nav>
  <!-- <router-view /> -->
</template>

<style lang="scss"></style>
