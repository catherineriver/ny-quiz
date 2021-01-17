<template>
  <div class="special-selectel-ny-question">
    <div class="special-selectel-ny-question__list">
      <Option
        v-for="(option, index) in data[this.questionIndex].options"
        :key="index"
        :index="index + 1"
        :option="option" />
    </div>
  </div>
</template>

<script>
import Option from './Option.vue';

export default {
  components: {
    Option,
  },
  props: {
    data: {
      type: Array,
    },
    questionIndex: {
      type: Number,
    },
  },
  name: 'Question',
  mounted() {
    // console.log(this.data[this.questionIndex].answerIndex);
  },
};
</script>

<style lang="stylus">
.special-selectel-ny-question
  padding-bottom: 30px;
  @media (max-width 520px)
    padding-bottom: 20px;
</style>
