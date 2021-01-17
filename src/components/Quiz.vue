<template>
  <div class="special-selectel-ny-quiz">
    <div class="special-selectel-ny-quiz__container">
      <div class="special-selectel-ny-quiz__gradient">
        <Header :stepLength="stepLength" :questionIndex="questionIndex" />
        <Question :questionIndex="questionIndex" :data="this.dataQuestion" />
      </div>
      <Months
        :months="this.dataQuestion[this.questionIndex].answers"
        :isPicked="isPicked"
        :pickedItem="pickedItem"
        :rigthAnswer="dataQuestion[this.questionIndex].answerIndex"
        @send-click="sendClick"
      />
      <Popup
        v-if="showPopup"
        :popupText="dataQuestion[this.questionIndex].popup"
        @next="onButtonNext"
      />
    </div>
  </div>
</template>

<script>
import confetti from 'canvas-confetti';
import Popup from './Popup.vue';
import Header from './Header.vue';
import Months from './Months.vue';
import Question from './Question.vue';
import data from '../data/data';
import * as Analytics from '../lib/analytics';

export default {
  name: 'Quiz',
  components: {
    Header,
    Question,
    Months,
    Popup,
  },
  data() {
    return {
      data,
      stepLength: 7,
      questionIndex: 0,
      dataQuestion: data.questions,
      pickedItem: null,
      isPicked: false,
      score: 0,
      showPopup: false,
      months: data.months,
    };
  },
  mounted() {
    console.log(this.dataQuestion[this.questionIndex].answers);
  },
  methods: {
    confettiStart() {
      const end = Date.now() + 0.5 * 1000;

      const colors = ['#ff77d0', '#e8e64a', '#0ce8d2', '#4f0dff', '#8b11ff'];

      (function frame() {
        confetti({
          particleCount: 10,
          angle: 60,
          spread: 55,
          origin: { x: 0.5 },
          colors,
        });
        confetti({
          particleCount: 10,
          angle: 120,
          spread: 55,
          origin: { x: 0.5 },
          colors,
        });

        if (Date.now() < end) {
          requestAnimationFrame(frame);
        }
      }());
    },
    reset() {
      this.pickedItem = null;
      this.isPicked = false;
    },
    onButtonNext() {
      this.showPopup = false;
      clearTimeout(this.timerQuestion);
      this.timerQuestion = setTimeout(() => {
        this.nextQuestion();
      }, 200);
    },
    sendClick(index) {
      this.$emit('send-click', index);
      if (this.questionIndex === 0) {
        Analytics.sendEvent('start');
      }
      if (this.dataQuestion[this.questionIndex].answerIndex === index) {
        Analytics.sendEvent(`answer-${this.questionIndex + 1}`);
        this.pickedItem = index;
        this.isPicked = true;
        this.score += 1;
        clearTimeout(this.timerQuestion);
        this.confettiStart();
        this.timerQuestion = setTimeout(() => {
          this.nextQuestion();
        }, 2000);
      } else {
        Analytics.sendEvent(`answer-${this.questionIndex + 1}`);
        this.pickedItem = index;
        this.isPicked = true;
        this.showPopup = true;
      }
    },
    nextQuestion() {
      if (this.questionIndex < 6) {
        Analytics.sendEvent(`next-${this.questionIndex + 1}`);
        this.questionIndex += 1;
        this.reset();
      } else {
        this.$emit('show-result', this.score);
      }
    },
  },
};
</script>

<style lang="stylus">
  .special-selectel-ny-quiz
    border-radius 8px;
    position: static;

    width: 100%;
    max-width 640px;

    z-index: 3;
    &__gradient
      position: relative;
      padding-top 20px;
      background: #FEEBEF;
      @media (min-width 640px)
        border-top-left-radius: 8px;
        border-top-right-radius: 8px;
</style>
