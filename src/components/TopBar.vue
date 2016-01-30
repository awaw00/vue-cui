<style lang='less'>
.top-bar{
  width: 100%;
  &.top-bar-fixed{
    position: fixed;
    top: 0;
    left: 0;
  }
}
</style>
<template lang='jade'>
div.top-bar.color-normal(:class="{'top-bar-fixed': fixed}", :style='{top: top}' v-show='show')
  slot
</template>
<script>
import './styles/common.less'
import './styles/transition.less'
import './styles/colorloop.less'
export default {
  props: {
    fixed: {
      type: Boolean,
      default: true
    },
    show: {
      type: Boolean,
      default: true
    },
    top: {
      type: Number,
      default: 0
    }
  }
}
</script>
