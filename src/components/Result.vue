<template>
  <div class="special-selectel-ny-result" ref="selectelResult">
    <div class="special-selectel-ny-result__score">
      <span>{{ this.score }} из 7. </span>{{ data.title }}
    </div>
    <div class="special-selectel-ny-result__image">
      <img v-if="$screen.width > 640" :src="data.image" alt="" />
      <img v-if="$screen.width < 640" :src="data.mobileImage" alt="" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'Result',
  props: {
    data: {
      type: Object,
    },
    score: {
      type: Number,
      default: 0,
    },
  },
  mounted() {
    setTimeout(() => {
      const scrollTo = (to, duration) => {
        const start = window.pageYOffset;
        const change = to - start;
        let currentTime = 0;
        const increment = 20;

        const animateScroll = () => {
          currentTime += increment;
          const val = Math.easeInOutQuad(currentTime, start, change, duration);
          window.scroll(0, val);
          if (currentTime < duration) {
            setTimeout(animateScroll, increment);
          }
        };
        animateScroll();
      };

      Math.easeInOutQuad = (t, b, c, d) => {
        t /= d / 2;
        if (t < 1) return (c / 2) * t * t + b;
        t -= 1;
        return (-c / 2) * (t * (t - 2) - 1) + b;
      };

      const scrollToElement = (ref) => {
        scrollTo(ref.getBoundingClientRect().top + window.scrollY - 100, 500);
      };

      scrollToElement(this.$refs.selectelResult);
    });
  },
};
</script>

<style lang="stylus">
.special-selectel-ny-result
  position: relative;
  flex-shrink: 0;
  background: #E25A76;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;

  font-weight: 500;
  font-size: 24px;
  line-height:29px;

  border-top-left-radius: 8px;
  border-top-right-radius: 8px;
  @media (max-width: 640px)
    font-size: 24px;
    line-height: 29px;
    border-radius 0;
  &__score
    color: #fff;
    padding: 0px 20px;
    max-width: 50%;
    @media (max-width: 640px)
      padding: 38px 15px;
      padding-right: 0;

  &__image
    max-width: 219px;
    flex-shrink: 0;
    @media (max-width: 640px)
      position: relative;
      max-width: 150px;
</style>
