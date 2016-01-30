<style lang='less'>
@import "./styles/color.less";
@import "./waves/waves.less";
.wave-button{
  &.wave-button-raised{
    box-shadow: 0px 4px 5px -2px rgba(0, 0, 0, 0.2), 0px 7px 10px 1px rgba(0, 0, 0, 0.14), 0px 2px 16px 1px rgba(0, 0, 0, 0.12);
  }
  &.wave-button-primary{
    .mixin-color-normal;
    .mixin-color-hover;
    .mixin-color-focus;
  }
  &.wave-button-accent{
    .mixin-color-accent-normal;
    .mixin-color-accent-hover;
    .mixin-color-accent-focus;
  }
  &.wave-button-sharp{
    border-radius: 0;
  }
  > a{
    width: 100%;
    height: 100%;
    display: block;
    color: inherit;
    padding: .1em .2em;
    text-decoration: none;
    text-align: center;
    &:hover, &:active, &:visited{
      color: inherit;
      text-decoration: none;
    }
  }
}
</style>
<template lang='jade'>
div.wave-button.waves-effect.waves-button(@click='btnClick', :class='btnStyle')
  a
    slot
</template>
<script>
import * as Waves from './waves/waves.js'
Waves.init()
export default {
  props: {
    vlink: {
      type: Object,
      default: null
    },
    btnType: {
      type: Array,
      default: []
    }
  },
  computed: {
    btnStyle () {
      let arr = []
      for (let i = 0; i < this.btnType.length; i++) {
        if (this.btnType[i] === 'raised') {
          arr.push('whiteframe-z3')
        } else {
          arr.push('wave-button-' + this.btnType[i])
        }
      }
      return arr
    }
  },
  methods: {
    btnClick () {
      this.$dispatch('btn-click')
    }
  }
}
</script>
