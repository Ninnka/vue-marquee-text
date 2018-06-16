<template>
  <div
    ref="marqueeTextWrap"
    class="marquee-text-wrap"
    :style="marqueeTextWrapStylesGetter">
    <span
      ref="marqueeText"
      class="text"
      :style="marqueeTextStylesGetter">
      {{ text }}
    </span>
  </div>
</template>

<script>
export default {
  name: 'MarqueeText',

  props: {
    text: {
      type: String,
      default: ''
    },

    isTag: {
      type: String,
      default: 'span'
    },

    animaDuration: {
      type: Number,
      default: -1, // *秒
    },

    nextRollDelay: {
      type: Number,
      default: 1000 // * 毫秒
    },

    deviationFactor: {
      type: Number,
      default: 6
    },

    enable: {
      type: Boolean,
      default: true, // * 默认开启动画
    }
  },

  data () {
    return {
      animaTranslateXEnd: 0,
      animaTranslateXEndSave: 0,
      nextRollTimer: null,
      durationCalced: 6, // * 默认是6
    };
  },

  computed: {
    marqueeTextStylesGetter () {
      const styles = {};
      if (this.animaTranslateXEndSave !== 0 && this.enable) {
        styles.transform = `translate3d(${this.animaTranslateXEnd}px, 0, 0)`;
        styles.transition = `transform ${this.animaDuration !== -1 ? this.animaDuration : this.durationCalced}s`;
      }
      return styles;
    },

    marqueeTextWrapStylesGetter () {
      const styles = {};
      if (this.animaTranslateXEndSave !== 0) {
        styles.boxShadow = `-1px 0px 0px 0px rgba(120, 120, 120, 0.25) inset`;
      }
      return styles;
    }
  },

  async mounted () {
    if (this.$refs.marqueeTextWrap && this.$refs.marqueeText) {
      const wrapBoundClient = this.$refs.marqueeTextWrap.getBoundingClientRect();
      const wrapWidth = wrapBoundClient.width;
      // console.log('wrapWidth', wrapWidth);
      const textBoundClient = this.$refs.marqueeText.getBoundingClientRect();
      const textWidth = textBoundClient.width;
      // console.log('textWidth', textWidth);
      if (wrapWidth < textWidth) {
        this.animaTranslateXEnd = this.animaTranslateXEndSave = wrapWidth - textWidth - this.deviationFactor;
        this.durationCalced = Math.ceil(-this.animaTranslateXEndSave / 30);
        this.$refs.marqueeText.addEventListener('transitionend', this.marqueeEnd);
      }
    }
  },

  async beforeDestory () {
    if (this.$refs.marqueeText) {
      this.$refs.marqueeText.removeEventListener('transitionend', this.marqueeEnd);
    }
    this.clearRollTimer();
  },

  methods: {
    marqueeEnd () {
      this.clearRollTimer();
      this.nextRollTimer = setTimeout(() => {
        if (this.enable) {
          if (this.animaTranslateXEnd !== 0) {
            this.animaTranslateXEnd = 0;
          } else {
            this.animaTranslateXEnd = this.animaTranslateXEndSave;
          }
        } else {
          this.clearRollTimer();
        }
      }, this.nextRollDelay);
    },

    clearRollTimer () {
      window.clearTimeout(this.nextRollTimer);
      this.nextRollTimer = null;
    }
  },
}
</script>

<style lang="less" scoped>
  .marquee-text-wrap {
    display: inline-block;
    overflow: hidden;
    max-width: 100%;

    .text {
      display: inline-block;
      pointer-events: none;
      white-space: nowrap;
    }
  }
</style>
