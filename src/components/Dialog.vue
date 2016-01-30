<style lang='less'>
.dialog-container{
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
    padding: 8px;
    background-color: white;
    z-index: 1002;
    position: fixed;
    left: 50%;
    top: 50%;
    transform: translateX(-50%) translateY(-50%);
  }
}
</style>
<template lang='jade'>
div.dialog-container
  div.dialog-background(v-show='show')
  div.dialog-body.whiteframe-z4(v-show='show', transition='bubble')
    slot
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
