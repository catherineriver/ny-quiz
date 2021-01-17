<template>
  <div :class="['special-selectel-ny-month',
    {'is-rightAnswer': pickedItem === index && rigthAnswer === index },
    {'is-wrongAnswer': pickedItem === index && rigthAnswer !== pickedItem},
    {'is-picked': pickedItem === index},
    {'is-answer': rigthAnswer === index}
    ]"
   @click="sendClick(index)"
   :style="isShow ? filterStyle : style">
    {{month.title}}
  </div>
</template>

<script>
export default {
  name: 'Month',
  data() {
    return {
      isShow: false,
    };
  },
  props: {
    month: {
      type: Object,
    },
    index: {
      type: Number,
    },
    rigthAnswer: {
      type: Number,
    },
    pickedItem: {
      type: Number,
    },
    bgColor: {
      type: String,
    },
  },
  computed: {
    filterStyle() {
      return `background-color: ${this.bgColor}` || 'red';
    },
    style() {
      return `background-color: ${this.bgColor}` || '#157E4C';
    },
  },
  methods: {
    sendClick(index) {
      if (this.rigthAnswer !== this.pickedItem) {
        this.isShow = true;
      }
      this.$emit('send-click', index);
    },
  },

};
</script>

<style lang="stylus">
.special-selectel-ny-month
  border-radius: 5px;

  font-weight: normal;
  font-size: 16px;
  line-height: 19px;
  text-align: center;
  color: #FFFFFF;
  background: #E25A76;

  padding 13px 0

  width: 100%;
  max-width: calc(25% - 12px);

  margin-bottom: 15px;

  @media (max-width 640px)
    max-width: calc(50% - 5px)

  &:hover
    cursor pointer
    opacity: 0.8
    @media (max-width 640px)
      opacity: 1
  &.is-disabled
    pointer-events: none;
    background #B8B8B8;

</style>
