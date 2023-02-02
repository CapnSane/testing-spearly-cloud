<script lang="ts">
import Header from "./components/Header.vue";
import Middle1 from "./components/Middle1.vue";
import Middle2 from "./components/Middle2.vue";
export default {
  components: {
    Header,
    Middle1,
    Middle2,
  },
};
</script>
<template>
  <nav>
    <Header />
    <Middle1 />
    <Middle2 />
    <!-- <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link> -->
  </nav>
  <!-- <router-view /> -->
</template>

<style lang="scss"></style>
