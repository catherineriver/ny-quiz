<template>
  <div class="special-appgallery-promo-shares">
    <div class="likely" ref='share'></div>
      <div :class="['special-appgallery-promo-shares__share', {'special-appgallery-promo-shares__share--copied':showModal}]"
          v-clipboard="clipboardCopyHandler()"
          v-clipboard:success="clipboardSuccessHandler" />
      <div class="special-appgallery-promo-shares__restart" @click="restart">
        <icon-base
            icon-name='icon-restart'
            width="17"
            height="17"
            viewBox="0 0 17 17">
            <icon-restart></icon-restart>
        </icon-base>
        Пройти ещё раз
      </div>
    </div>
</template>

<script>
import IconBase from './IconBase.vue';
import IconRestart from './Icons/IconRestart.vue';

import * as Analytics from '../lib/analytics';
import * as Share from '../lib/share';

export default {
  name: 'ShareBlock',
  components: {
    IconRestart,
    IconBase,
  },
  data() {
    return {
      showModal: false,
    };
  },
  props: {
    score: {
      type: Number,
    },
  },
  mounted() {
    this.share();
  },
  methods: {
    clipboardCopyHandler() {
      this.url = `https://vc.ru/special/year-test/share/${this.score}`;
      return this.url;
    },
    clipboardSuccessHandler({ value, event }) {
      this.value = value;
      this.event = event;
      Analytics.sendEvent('share-link');
      clearTimeout(this.modalTimeout);
      this.showModal = true;
      this.modalTimeout = setTimeout(() => {
        this.showModal = false;
      }, 1500);
    },
    declineWord(number, words) {
      let result = '';

      if (number % 10 === 1 && number % 100 !== 11) {
        result += words[0];
      } else if ([2, 3, 4].indexOf(number % 10) > -1 && [12, 13, 14].indexOf(number % 100) < 0) {
        result += words[1];
      } else {
        result += words[2];
      }

      return result;
    },
    share() {
      const socials = this.$refs.share;
      Share.make(socials, {
        title: 'Угадайте месяц 2020 года по нашим заголовкам',
        url: `https://vc.ru/special/year-test/share/${this.score}`,
      });
    },
    restart() {
      Analytics.sendEvent('Restart');
      this.$root.$emit('restart');
    },
  },
};
</script>

<style lang="stylus">
.special-appgallery-promo-shares
  display: flex;
  flex-flow: row wrap;
  margin-top: 20px;
  &__restart
    display flex
    flex-direction row
    align-items center

    font-size: 16px;
    line-height: 19px;
    cursor: pointer;
    color: #E25A76;
    & > svg
      color: #E25A76;
      margin-right 10px
      transition: transform 0.4s ease-in;
    &:hover
      & > svg
        transform: rotate(360deg);
    @media (max-width 893px)
      margin: 30px auto;
  &__share
    z-index 10
    position relative
    background-image: url("data:image/svg+xml,%3Csvg width='16' height='16' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M5.464 4.534l1.708-1.708v9.036a.828.828 0 001.656 0V2.826l1.708 1.708a.828.828 0 101.17-1.17L8.586.241a.828.828 0 00-1.171 0L4.294 3.363a.828.828 0 101.17 1.17z' fill='%23E25A76'/%3E%3Cpath d='M15.172 7.172a.828.828 0 00-.827.828v6.345H1.655V8A.828.828 0 100 8v6.62A1.38 1.38 0 001.38 16h13.24A1.38 1.38 0 0016 14.62V8a.828.828 0 00-.828-.828z' fill='%23E25A76'/%3E%3C/svg%3E");
    background-repeat: no-repeat;
    background-position: center;

    margin: 0 14px;

    border: 1px solid #FBB6C4;
    box-sizing: border-box;
    border-radius: 5px;
    cursor pointer

    transition: background .2s

    height: 45px;
    width: 100%;
    max-width 45px
    box-sizing: border-box;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    outline: none;
    cursor: pointer;

    -webkit-transition: all 0.2s;
    transition: all 0.2s;
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
      cursor: pointer;
      box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
    &:hover::after
      opacity: 1;
      @media (max-width 640px)
        opacity: 0;
    @media (max-width 320px)
      margin: 30px 0;

    &--copied::before
      content 'Cсылка скопирована'
      background: #E25A76;

      border-radius: 3px;
      position: absolute;
      bottom: 50px;
      right: 0;

      padding: 6px 8px;
      font-size: 12px;
      line-height: 12px;
      display: block;

      width: 140px;
      transform: translateX(45px);
      color: #fff;

      @media (max-width: 320px)
        right: 30px;

.likely
  z-index: 10;
  flex-shrink: 0;
.likely__counter
  display: none;
.likely--custom
  display flex
  flex-direction row
  align-items center
  width: 100%;
  margin: 0 -7px;

  & .likely__widget
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;

    flex: 1 1 auto;
    margin: 0 7px;

    height: 45px;
    font-size: 14px;
    color: #e25a76;

    padding: 0 12px;

    background: #FFFFFF;
    border: 1px solid #FBB6C4;
    box-sizing: border-box;
    border-radius: 4px;

    box-sizing: border-box;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    outline: none;
    cursor: pointer;

    -webkit-transition: all 0.2s;
    transition: all 0.2s;
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
      cursor: pointer;
      box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
    &:hover::after
      opacity: 1;
      @media (max-width 640px)
        opacity: 0;
    & .likely__icon
        fill: currentColor;
        flex-shrink: 0;
        display: flex;
        align-items: center;
        justify-content: center;
        & > svg
            width: 20px;
            height: 20px;
  & .likely__widget--facebook
    max-width: 150px;
    padding: 7px 20px;
    & svg
      width: 22px;
      height: 21px;
      margin-right: 10px;

</style>
