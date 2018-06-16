<template>
  <div id="app">
    <marquee-text class="mt" :text="text">
    </marquee-text>
  </div>
</template>

<script>
import MarqueeText from './components/marquee-text';

export default {
  name: 'App',

  components: {
    MarqueeText
  },

  data () {
    return {
      text: 'Lorem ipsum, dolor sit amet consectetur adipisicing elit. Voluptatem assumenda eos incidunt consequatur optio iusto, obcaecati voluptatum sapiente libero ipsa explicabo nihil et tempore quaerat repellendus aperiam, numquam totam ex.',
    };
  }
};
</script>

<style lang="less">
#app {
  font-family: "PingFangSC-Regular","PingFang SC","Helvetica Neue",Helvetica,"Hiragino Sans GB","Microsoft YaHei","微软雅黑",Arial,sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  -webkit-overflow-scrolling: touch;
  -webkit-backface-visibility: hidden;
  -moz-backface-visibility: hidden;
  -ms-backface-visibility: hidden;
  backface-visibility: hidden;
  -webkit-perspective: 1000;
  -moz-perspective: 1000;
  -ms-perspective: 1000;
  perspective: 1000;
  -webkit-transform: translateZ(0);
  -moz-transform: translateZ(0);
  -ms-transform: translateZ(0);
  -o-transform: translateZ(0);
  transform: translateZ(0);
  margin: 0 auto;
  width: 100%;
  height: 100%;
  max-width: 470px;
  max-height: 850px;
  display: block;
  background: #eeeeee;
  overflow: hidden;
  font-size: 0.12rem;
  position: relative;
}

.mt {
  vertical-align: middle;
  font-size: 16px;
  color: #272727;
  font-weight: 600;
  // max-width: 200px;

}

</style>
