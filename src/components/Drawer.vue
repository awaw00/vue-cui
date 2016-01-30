<style lang="less">
.drawer-container{
  position: relative;
  z-index: 2000;
  .drawer-background{
    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    z-index: 1;
    background-color: rgba(0, 0, 0, 0.65);
  }
  .drawer-body{
    background-color: #FFFFFF;
    box-shadow: 0px 0px 10px 2px rgba(49, 50, 49, 0.49);
    position: fixed;
    z-index: 2;
    &.drawer-left{
      left: 0;
      top: 0;
      bottom: 0;
    }
    &.drawer-right{
      right: 0;
      top: 0;
      bottom: 0;
    }
    &.drawer-top{
      left: 0;
      right: 0;
      top: 0;
    }
    &.drawer-bottom{
      left: 0;
      right: 0;
      bottom: 0;
    }
  }
}
</style>
<template lang='jade'>
div.drawer-container
  div.drawer-background(@click='clickOutSide', v-show='show')
  div.drawer-body(v-show='show', :transition='transition', :class='bodyStyle', :style='{"width": placement === "left" || placement == "right" ? size + "%" : auto, "height": placement === "top" || placement === "bottom" ? size + "%" : auto }')
    slot
</template>
<script>
import './styles/common.less'
import './styles/transition.less'
export default {
  props: {
    placement: {
      type: String,
      default: 'left'
    },
    size: {
      type: Number,
      default: 100
    },
    show: {
      type: Boolean,
      default: false,
      twoWay: true
    }
  },
  data () {
    return {
      bodyStyle: {
        'drawer-left': this.placement === 'left',
        'drawer-right': this.placement === 'right',
        'drawer-top': this.placement === 'top',
        'drawer-bottom': this.placement === 'bottom'
      }
    }
  },
  computed: {
    transition () {
      return 'drawer-' + this.placement
    }
  },
  methods: {
    clickOutSide () {
      this.show = false
    }
  }
}
</script>
