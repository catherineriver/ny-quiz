<template>
  <div class="special-selectel-ny-header">
    <div class="special-selectel-ny-header__container">
      <div class="special-selectel-ny-header__title">Угадайте месяц 2020 года по заголовкам vc.ru</div>
      <div class="special-selectel-ny-header__counter"><span>{{questionIndex + 1}}</span> / {{stepLength}}</div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Header',
  data() {
    return {
      data: {
        canvas: null,
      },
    };
  },
  props: {
    questionIndex: {
      type: Number,
    },
    stepLength: {
      type: Number,
    },
  },
};
</script>

<style lang="stylus">
.special-selectel-ny-header
  &__container
    display flex
    align-items center
    justify-content space-between
    padding-bottom 8px;

    padding-left 20px
    padding-right 35px
    @media (max-width 640px)
      padding-left 15px
      padding-right 15px
    @media (max-width 520px)
      padding-bottom 10px;

  &__counter
    flex-shrink: 0;
    font-size: 16px;
    line-height: 22px;

    color: #000;
    & > span
      font-weight: bold;
      font-size: 18px;
      color: #e25a76;
  &__title
    font-size: 22px;
    line-height: 27px;
    color: #000000;
    font-weight: 500;

    @media (max-width 640px)
      font-size: 22px;
      line-height: 26px;
      margin-right: 10px;

</style>
