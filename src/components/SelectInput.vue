<style lang='less'>
@import "./icons/iconfont.less";
@default-color: #FF5722;
.select-input{
  font-size: 20px;
  position: relative;
  > label{
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    font-size: 1.2em;
    transition: .2s ease all;
    z-index: 1;
    &.label-shrink{
      font-size: 0.8em;
      margin-top: -1.2em;
      color: @default-color;
    }
    &.label-spread{
      font-size: 1.2em;
      margin-top: 0;
      color: rgb(166, 166, 166);
    }
  }
  > span{
    vertical-align: bottom;
    position: relative;
    display: block;
    height: 2em;
    line-height: 2em;
    border-bottom: 1px solid rgb(166, 166, 166);
    z-index: 1;
    .iconfont{
      float: right;
      transition: ease all .3s;
      transform-origin: center;
      &.reversal{
        transform: rotate(180deg);
      }
    }
  }
  > .select-input-border{
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    border-bottom: 2px solid @default-color;
  }
  > .select-options{
    position: absolute;
    width: 100%;
    top: 110%;
    left: 0;
    right: 0;
    background-color: #FFFFFF;
    overflow: hidden;
    z-index: 3;
    > .select-option{
      padding: 8px;
      &:hover{
        background-color: @default-color;
        color: contrast(@default-color, black, white, 50%);
      }
      padding: 3px 10px;
    }
  }
  > .select-input-mask{
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 2;
  }
}
</style>
<template lang='jade'>
div.select-input
  label(:class='{"label-shrink": selected, "label-spread": !selected}') {{label}}
  span(@click='show = true') {{value}}
    span.iconfont(:class='{"reversal": show}') &#xe601;
  div.select-input-border(v-show='show', :transition='borderTransition')
  div.select-options.whiteframe-z2(v-show='show', :transition='optionsTransition')
    div.select-option(v-for='o in options', @click='selectOption(o)') {{o.value}}
  div.select-input-mask(v-show='show', @click.stop='show = false')
</template>
<script>
import './styles/common.less'
import './styles/transition.less'
import './styles/colorloop.less'
export default {
  props: {
    label: {
      type: String,
      default: 'Select Input'
    },
    show: {
      type: Boolean,
      default: false,
      twoWay: true
    },
    useTransition: {
      type: Boolean,
      default: true
    },
    value: {
      twoWay: true
    },
    key: {
      twoWay: true
    },
    options: {
      type: Array,
      default: [
        { key: 1, value: '我'},
        { key: 2, value: '是'},
        { key: 3, value: '谁'}
      ]
    }
  },
  data () {
    return {
      active: false
    }
  },
  computed: {
    borderTransition () {
      return this.useTransition ? 'input-border' : ''
    },
    optionsTransition () {
      return this.useTransition ? 'list' : ''
    },
    selected () {
      return this.value && this.value.length >= 1
    }
  },
  methods: {
    selectOption (o) {
      this.value = o.value
      this.key = o.key
      this.show = false
    }
  }
}
</script>
