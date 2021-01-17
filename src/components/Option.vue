<template>
  <div class="special-selectel-ny-option">
    <div class="special-selectel-ny-option__title">
      {{option.title}}
    </div>
  </div>
</template>

<script>
export default {
  name: 'Option',
  props: {
    option: {
      type: Object,
    },
    index: {
      type: Number,
    },
  },
};
</script>

<style lang="stylus">
.special-selectel-ny-option
  position relative
  font-size: 16px;
  line-height: 23px;

  color: #000;
  background: #FBDFE5;

  padding: 13px 0;
  margin: 10px 0;
  @media (max-width 640px)
    font-size: 18px;
    line-height: 23px;

  @media (max-width 520px)
    font-size: 16px;
    line-height: 21px;

    padding: 10px 0;
    margin: 10px 0;

  &__title
    padding-left 20px
    padding-right 35px
    @media (max-width 640px)
      padding-left: 15px;
</style>
