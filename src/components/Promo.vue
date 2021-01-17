<template>
  <div :class="['special-selectel-ny-promo']">
    <Result :data="data" :score="score"/>
    <PromoContent :score="score"/>
  </div>
</template>

<script>
import Result from './Result.vue';
import PromoContent from './PromoContent.vue';

export default {
  name: 'Promo',
  components: {
    Result,
    PromoContent,
  },
  props: {
    data: {
      type: Object,
    },
    score: {
      type: Number,
      default: 0,
    },
  },
};
</script>

<style lang="stylus">
.special-selectel-ny--page
  .special-selectel-ny-promo
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
.special-selectel-ny-promo
  border-radius 8px;
  position: relative;

  width: 100%;
  max-width 640px;
  z-index: 10;
</style>
