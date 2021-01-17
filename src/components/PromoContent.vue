<template>
  <div class="special-selectel-ny-content">
    <div class="special-selectel-ny-content__logo">
      <img src="https://leonardo.osnova.io/cf1eecc7-a296-5893-8210-9958732acc8d/" alt="">
    </div>
    <div class="special-selectel-ny-content__desc">
      <p>Все материалы vc.ru живут в&nbsp;Облачном хранилище Selectel. Это провайдер
      инфраструктуры с&nbsp;собственными дата-центрами, обслуживающий vc.ru уже
      9&nbsp;лет. Так что можем поручиться за&nbsp;надёжность их&nbsp;продуктов.</p>
      <p>Selectel предлагает современные серверы и&nbsp;актуальные managed-решения&nbsp;&mdash;
      не&nbsp;придётся думать об&nbsp;администрировании. А&nbsp;также много других услуг,
      которые уже оценили &laquo;Ситимобил&raquo;, ЦИАН, группа ПИК, Ostrovok.ru
      и&nbsp;ещё более 18&nbsp;тысяч клиентов.</p>
    </div>
    <a href='https://selectel.ru' target="_blank"
      @click="sendAnalytics"
      class="special-selectel-ny-content__button">
      Подобрать услугу
    </a>
    <ShareBlock :score="score"/>
  </div>
</template>

<script>
import ShareBlock from './ShareBlock.vue';
import * as Analytics from '../lib/analytics';

export default {
  name: 'PromoContent',
  components: {
    ShareBlock,
  },
  props: {
    score: {
      type: Number,
    },
  },
  methods: {
    sendAnalytics() {
      Analytics.sendEvent('Final-promo');
    },
  },
};
</script>

<style lang="stylus">
.special-selectel-ny-content
  background: #FFFFFF;
  border-bottom-left-radius: 8px;
  border-bottom-right-radius: 8px;

  padding: 30px 20px;
  @media (max-width: 640px)
    border-radius: 0;
    padding: 20px 15px 0;
  &__logo
    max-width: 90px;
    width: 100%;
    margin-bottom: 25px;
    @media (max-width: 640px)
      max-width 90px
      margin-bottom:15px;
  &__desc
    font-weight: normal;
    font-size: 16px;
    line-height: 24px;
    & p + p
      margin-top: 1em;
  &__button
    margin-top: 20px;

    display: flex;
    align-items: center;
    flex-direction: row;
    justify-content: center;
    flex-basis: 50%;

    font-weight: 500;
    font-size: 16px;
    line-height 45px;
    border-radius: 5px;
    max-width: 184px;

    background: #E25A76;
    color: #fff;
    box-sizing: border-box;

    text-decoration: none;

    transition: background .2s, color .2s, border .2s, box-shadow 0.2s
    &:hover
      background: #fff;
      color: #E25A76;
      box-shadow inset 0px 0px 0px 1px #E25A76
    @media (max-width: 640px)
      max-width: none;
      margin-bottom:35px;
</style>
