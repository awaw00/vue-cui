<style lang='less'>
@default-color: #FF5722;
.progress-bar-container{
  width: 100%;
  height: .5em;
  background-color: lighten(@default-color, 30%);
  .progress-bar{
    transition: all ease .2s;
    width: 0%;
    height: 100%;
    box-shadow: none;
    background-color: @default-color;
  }
}
</style>
<template lang='jade'>
div.progress-bar-container
  div.progress-bar(:style='{ width: percentage + "%" }')
</template>
<script>
import './styles/colorloop.less'
export default {
  props: {
    percentage: {
      type: Number,
      default: 0
    }
  }
}
</script>
