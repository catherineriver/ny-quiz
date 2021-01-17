<template>
  <div class="special-selectel-ny-popup">
      <div class="special-selectel-ny-popup__title">Мимо!</div>
      <div class="special-selectel-ny-popup__text">{{popupText}}</div>
      <div class="special-selectel-ny-popup__button" @click="nextQuestion">Дальше</div>

  </div>
</template>

<script>
export default {
  name: 'Popup',
  props: {
    popupText: {
      type: String,
    },
  },
  methods: {
    nextQuestion() {
      this.$emit('next');
    },
  },
};
</script>

<style lang="stylus">
.special-selectel-ny-popup
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);

  width: 100%;
  max-width: 506px;
  height: 216px;
  z-index: 10;
  background: #FFFFFF;
  box-shadow: 0px 0px 50px -20px rgba(0, 0, 0, 0.75);
  border-radius: 30px;

  display: flex;
  align-items: center;
  flex-flow column nowrap

  @media (max-width 640px)
    max-width: 342px;
    height: 242px;
  &::before
    content: ''
    width: 100%;
    max-width: 490px;
    height: 200px;
    position: absolute;
    top: 8px;
    left: 8px;

    display: block;
    border: 2px solid #FBB6C4;
    border-radius: 23px;
    @media (max-width 640px)
      height: 226px;
      max-width: 95%;
    @media (max-width 320px)
      max-width: 303px;
  &__title
    font-weight: 500;
    font-size: 30px;
    line-height: 35px;

    color: #E25A76;
    padding 30px 0 15px
  &__text
    font-weight: normal;
    font-size: 18px;
    line-height: 26px;
    padding-bottom 25px;

    @media (max-width 640px)
      padding: 0 30px;

  &__button
    background: #fff;
    border-radius: 5px;
    color #E25A76;
    max-width: 111px;
    width: 100%;
    border: 1px solid #E25A76;
    box-sizing: border-box;
    border-radius: 5px;

    font-weight: 500;
    font-size: 16px;
    line-height 45px
    text-align center
    box-sizing: border-box;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    outline: none;
    cursor: pointer;

    -webkit-transition: all 0.2s;
    transition: all 0.2s;
    z-index 1
    @media (max-width 640px)
      margin-top 25px;
    &:after
      content: "";
      border-radius: 5px;
      position: absolute;
      z-index: -1;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;

      opacity: 0;
      -webkit-transition: all 0.2s;
      transition: all 0.2s;
    &:hover
      box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);

    &:hover::after
      opacity: 1;


</style>
