<template>
  <div
    :class="[
      'special-selectel-ny-months',
      { 'is-rightAnswer': isPicked && pickedItem === rigthAnswer },
      { 'is-wrongAnswer': isPicked && pickedItem !== rigthAnswer },
    ]"
  >
    <Month
      v-for="(month, index) in months"
      :key="index"
      :index="index"
      :month="month"
      :rigthAnswer="rigthAnswer"
      :pickedItem="pickedItem"
      :bgColor="month.color"
      @send-click="sendClick"
    />

  </div>
</template>

<script>
import Month from './Month.vue';

export default {
  name: 'Months',
  components: {
    Month,
  },
  props: {
    months: {
      type: Array,
    },
    pickedItem: {
      type: Number,
    },
    isPicked: {
      type: Boolean,
    },
    rigthAnswer: {
      type: Number,
    },
  },
  methods: {
    sendClick(index) {
      this.$emit('send-click', index);
    },
  },
  mounted() {
    console.log(this.months);
  },
};
</script>

<style lang="stylus">
.special-selectel-ny-months
  position relative

  background: #FEEBEF;
  display flex
  flex-flow: row wrap;
  justify-content: space-between;

  padding 0 15px;

  @media (min-width 640px)
    padding 0 20px;
    border-bottom-left-radius: 8px;
    border-bottom-right-radius: 8px;

  &.is-rightAnswer > .special-selectel-ny-month
    background-color #E25A76 !important
    pointer-events none
  &.is-wrongAnswer > .special-selectel-ny-month.is-answer
    background-color #157E4C !important
    opacity 1
    @media (max-width 640px)
      background-color #E25A76 !important
  &.is-rightAnswer > .special-selectel-ny-month.is-rightAnswer
    background-color #157E4C !important
    opacity 1
  &.is-wrongAnswer > .special-selectel-ny-month
    background-color #E25A76 !important
    opacity .2
    pointer-events none
  &.is-wrongAnswer > .special-selectel-ny-month.is-wrongAnswer
    background-color #E25A76 !important
    opacity 1
  &.is-wrongAnswer > .special-selectel-ny-month.is-rightAnswer
    background-color #157E4C !important
</style>
