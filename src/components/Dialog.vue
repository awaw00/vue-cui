<style lang='less'>
.dialog-container{
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  z-index: 1000;
  .dialog-background{
    position: fixed;
    left: 0;
    right: 0;
    bottom: 0;
    top: 0;
    background-color: rgba(0, 0, 0, 0.6);
    z-index: 1001
  }
  .dialog-body{
    padding: 16px;
    background-color: white;
    z-index: 1002;
    position: relative;
    margin: 0 auto;
    width: 360px;
    top: 160px;
    top: 20vh;
  }
}
</style>
<template lang='jade'>
div.dialog-container(v-show='show', transition='fade')
  div.dialog-background(v-show='show')
  div.dialog-body.whiteframe-z4(v-show='show', transition='dialog')
    slot
    div.clearfix
</template>
<script>
import './styles/transition.less'
import './styles/common.less'
export default {
  props: {
    show: {
      type: Boolean,
      default: false
    }
  }
}
</script>
