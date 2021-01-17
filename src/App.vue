<template>
  <div
    :class="[
      'special-selectel-ny',
      `special-selectel-ny--${$store.state.params.location}`,
      {'l-mb-28': isFeed},
      {'l-island-round': isFeed},
    ]"
    v-observe-visibility="{
      callback: visibilityChanged,
      once: true,
    }"
  >
    <div :class="['special-selectel-ny__container', { result: isResult }]">
      <Quiz v-if="!isResult" @show-result="showResult" />
      <Promo
        v-if="isResult"
        :data="data.results[this.score]"
        :score="this.score"
        @restart="restart"
      />
    </div>
  </div>
</template>

<script>
import Quiz from './components/Quiz.vue';
import Promo from './components/Promo.vue';
import * as Analytics from './lib/analytics';
import { preloadImages } from './lib/helper';
import data from './data/data';

export default {
  name: 'App',
  components: {
    Quiz,
    Promo,
  },
  data() {
    return {
      data,
      isResult: false,
      score: 0,
      isFeed: false,
    };
  },
  methods: {
    visibilityChanged(isVisible) {
      if (isVisible) {
        Analytics.sendEvent('Project', 'Show');
      }
    },
    showResult(score) {
      console.log('result');
      this.isResult = true;
      this.score = score;
    },

    restart() {
      this.score = 0;
      this.isResult = false;
    },
  },
  mounted() {
    if (this.$store.state.params.location === 'feed') {
      this.isFeed = true;
    }
    this.$root.$on('restart', () => {
      this.restart();
    });
    preloadImages([
      'https://leonardo.osnova.io/3371525d-3304-5751-97a9-08dd5011bda0/',
      'https://leonardo.osnova.io/ffa60c66-d26e-5f1a-a62b-dc21f37b3a7b/',
      'https://leonardo.osnova.io/e9f5a372-98b6-5942-a574-ac4bd706cf63/',
      'https://leonardo.osnova.io/008630a2-8ae3-5dd7-b60d-79bb940fed6c/',
      'https://leonardo.osnova.io/22e1f030-1b37-57b2-870b-0f0cbdb336b2/',
      'https://leonardo.osnova.io/92b5ccb9-4f1c-5c52-8972-6e704f2281a5/',
      'https://leonardo.osnova.io/20d1d9cd-6450-52bb-9fe6-08db1ec2c24d/',
    ]);
  },
};
</script>

<style lang="stylus">
.live-stream {
  display: none;
}
.special-selectel-ny--page > .special-selectel-ny-quiz {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
@media (max-width 640px) {
  .special-selectel-ny--page > .special-selectel-ny-quiz {
    position: static;
    width: 100%;
    max-width: 640px;
    transform: none;
  }
}

.special-selectel-ny {
  -webkit-tap-highlight-color: transparent;
  -webkit-user-select: none;
  -ms-user-select: none;
  user-select: none;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  position: relative;
  z-index: 99;
  max-width: 100%;
  font-family: 'Roboto', sans-serif;
  font-size: 16px;
  line-height: normal;
  text-size-adjust: 100%;
  background-color: transparent;
  overflow: hidden;

  & *, & *:before, & *:after {
    box-sizing: border-box;
  }

  & svg {
    display: block;
    fill: currentColor;
    pointer-events: none;
  }

  & b {
    font-weight: 700;
  }

  & img {
    width: 100%;
    display: block;
  }

  & button {
    margin: 0;
    padding: 0;
    font-family: inherit;
    user-select: none;
    outline: none;
    box-shadow: none;
    appearance: none;
    cursor: pointer;
  }
  &__container {
    width: 640px
    max-width: 100%
    margin: 0 auto
    padding: 0 15px

    border-radius 8px;
    @media (max-width 520px) {
      padding 0;
    }
  }
  &--page {
    height: calc(100vh - 60px);
    display: flex;
    align-items: center;
    justify-content: center;
  }
  &--feed {
    & > .special-selectel-ny__container {
      width: 640px
      max-width: 100%
      margin: 0 auto

      border-radius 8px;
      height: auto;
      padding 0;

    }
    & > .special-selectel-ny__container::before,
    & > .special-selectel-ny__container::after {
      content: none;
    }
  }
  &__snowdrift {
    background-image: url("data:image/svg+xml,%3Csvg width='1920' height='359' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath fill-rule='evenodd' clip-rule='evenodd' d='M1983.01 136v223H-172.988V138.193c-.027-1.342 0-2.193 0-2.193 2.886-11.534 14.483-21.643 25.283-27.096 29.829-15.038 61.442-15.247 93.677-15.46 4.294-.028 8.599-.057 12.912-.12 20.906-.313 39.15-8.208 57.284-16.056 13.22-5.72 26.38-11.416 40.472-14.13 21.536-7.195 38.656-2.002 59.647 6.654 31.131 12.82 63.517 21.043 96.993 12.117 17.684-4.706 33.197-13.427 48.527-22.045 23.616-13.276 46.799-26.309 76.818-24.045 25.353 1.935 49.301 10.898 73.11 19.81 18.123 6.784 36.166 13.537 54.687 17.138 50.214 9.737 93.559-1.948 141.429-15.255.109-.054.272-.054.381-.054 33.095-10.387 67.007-19.367 101.791-19.746 11.966-.15 24.1.72 36.261 1.59 23.083 1.651 46.266 3.31 68.584-1.969 7.948-2.992 15.92-6.155 23.929-9.333 25.723-10.207 51.821-20.562 78.68-25.884C935.196-1.4 950.68-.21 966.11 3.306a.903.903 0 00.112-.01c.096-.012.21-.027.324.01 40.934 8.864 82.064 24.51 123.434 40.246 95.99 36.511 193.26 73.512 292.4 27.43 11.48-5.348 21.8-12.277 31.91-19.072 22.02-14.787 43.08-28.935 73.15-24.747 13.59 1.876 26.48 6.593 39.37 11.309 8.67 3.173 17.34 6.346 26.22 8.653 15.05 3.895 30.48 5.897 45.85 7.844 16.27 2.082 33 2.772 49.73 3.462 18.49.762 36.99 1.525 54.9 4.166 4.26-.09 8.53-.147 12.8-.203 11.2-.149 22.41-.297 33.54-1.041 3.42-.235 6.83-.478 10.25-.72 18.64-1.324 37.34-2.651 56-2.743 38.98-.162 76.49 9.034 110.78 27.644 10.02 5.421 19.03 15.209 28.13 25.11 8.89 9.661 17.88 19.43 28 25.356z' fill='%23fff'/%3E%3C/svg%3E");
    background-size: cover;
    background-repeat: no-repeat;
    width: 100%;
    height: 8vh;
    display: block;
    position: absolute;
    bottom 0;
    z-index 1

    animation: snowdrift 50s ease-in both;

    @media (max-width 640px){
      display: none;
    }
  }
}

@-webkit-keyframes snowdrift {
  0% {
    height: 8vh;
  }
  100% {
    height: calc((100vh - 662px) / 2);
  }
}
</style>
