<script lang="js">

  let stepFactor = 0.2;
  let randomNum = (Math.floor(Math.random() * 6) + 1)*stepFactor;

// export type Percentage = {
//   percentage: number;
// };

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
      if (this.percentage > 100) this.percentage = 100;
      else if (this.percentage < 100) this.percentage += randomNum;
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
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 29px;
}

.container {
  text-align: right;
}

.loading-bar {
  position: relative;
  width: 400px;
  height: 30px;
  border-radius: 4px;
  border: 1px solid #4797ff;
  overflow: hidden;

  .percentage {
    position: absolute;
    display: block;
    height: 100%;
    // border-radius: 4px;
    background-color: #4797ff70;
    animation: animate-stripes 3s linear infinite;
  }
}

.pb__text {
  color: #fff;
  font-size: 12px;
  margin: auto;
  width: max-content;
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
