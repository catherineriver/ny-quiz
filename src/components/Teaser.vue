<template>
  <div class="special-selectel-ny" @click="startTest">
    <div class="special-selectel-ny__container">
      <div class="special-selectel-ny__title">
        Угадайте месяц 2020 года по заголовкам vc.ru
      </div>
      <div class="special-selectel-ny__image">
        <img src="https://leonardo.osnova.io/8ce893e4-fb37-5042-8f30-d8ce74dbebfb/" alt="">
      </div>
    </div>
  </div>
</template>

<script>
import * as Analytics from '../lib/analytics';

export default {
  name: 'Teaser',
  methods: {
    startTest() {
      Analytics.sendEvent('Start');
      this.$emit('start-test');
    },
  },
};
</script>

<style lang="stylus">
.special-selectel-ny
  &__container
    overflow: hidden;
    width 100%
    max-width: 640px
    &:hover
      cursor pointer
</style>
