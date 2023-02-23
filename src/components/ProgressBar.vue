<script lang="ts">
// export type Percentage = {
//   percentage: number;
// };

let randomNum = Math.floor(Math.random() * 3) + 1;

// export type Props = {
//   fileName?: string;
// };

// const props = withDefaults(defineProps<Props>(), {
//   fileName: "file",
// });

export default {
  name: "ProgressBar",
  props: {
    fileName: { type: String, default: "file.zip" },
  },
  data: () => {
    return {
      percentage: 0,
    };
  },
  created() {
    var interval = setInterval(() => {
      if (this.percentage < 100) this.percentage += 0.1 * randomNum;
      else clearInterval(interval);
    }, 5);
  },
  computed: {
    percent() {
      return this.percentage.toFixed();
    },
  },
};
</script>

<template>
  <div class="pb__app">
    <div class="container">
      <div class="loading-bar">
        <div class="percentage" :style="{ width: percentage + '%' }">
          <p class="pb__text">{{ fileName }} {{ percent }}%</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.pb__app {
  font-family: Arial, Helvetica, sans-serif;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 20px;
}

.container {
  text-align: right;
  font-size: 8rem;
}

.loading-bar {
  position: relative;
  width: 400px;
  height: 30px;
  border-radius: 4px;
  border: 1px solid #4797ff;
  overflow: hidden;
  // border-bottom: 1px solid #ddd;
  // box-shadow: inset 0 1px 2px rgba($color: #000, $alpha: 0.4), 0 -1px 1px #fff, 0 1px 0 #fff;

  .percentage {
    position: absolute;
    display: block;
    height: 100%;
    border-radius: 4px;
    background-color: #4797ff70;
    animation: animate-stripes 3s linear infinite;
  }
}

.pb__text {
  color: #fff;
  font-size: 12px;
  margin: auto;
  width: fit-content;
  padding: 8px;
}

@keyframes animate-stripes {
  0% {
    background-position: 0 0;
  }
  100% {
    background-position: 60px 0;
  }
}
</style>
