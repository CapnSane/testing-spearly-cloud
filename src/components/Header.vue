<template>
  <div class="h-container">
    <div class="center">
      <router-link class="h-link" to="/">Home</router-link>
      <router-link class="h-link" to="/images">Images</router-link>
      <router-link class="h-link" to="/external" target="_blank">Another Page</router-link>
      <router-link class="h-link" to="/about">About</router-link>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import "@/assets/global.scss";
.h-container {
  display: flex;
  border: 1px solid brown;
  height: 40px;
  background-color: #ccaf4f69;
}

.h-link {
  margin: 0 10px;
}
</style>
