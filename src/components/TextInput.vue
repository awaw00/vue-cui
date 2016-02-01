<style lang='less'>
@default-color: #FF5722;
.text-input{
  position: relative;
  min-height: 2em;
  max-height: 2em;
  margin-top: 20px;
  label{
    position: absolute;
    left: 0;
    top: 0;
    transition: .2s ease all;
    z-index: 2;
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
  input{
    border: none;
    position: absolute;
    left: 0;
    bottom: 0;
    right: 0;
    border-bottom: 1px solid rgb(166, 166, 166);
    width: 100%;
    height: 2em;
    font-size: 1em;
    z-index: 1;
    &, &:focus{
      outline-offset: 0;
      outline: 0;
    }
  }
  .text-input-border{
    position: absolute;
    z-index: 2;
    left: 0;
    right: 0;
    bottom: 0;
    height: 0;
    border-bottom: 2px solid @default-color;
  }
  .text-input-mask{
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    z-index: 10;
  }
}

</style>
<template lang='jade'>
div.text-input
  label(:class='{"label-shrink": labelShrink, "label-spread": !labelShrink}') {{label}}
  div.text-input-mask(@click.stop='getFocus', v-show='!focused')
  input(:type='contentType', @focus='getFocus', v-model='content', @blur='lostFocus')
  div.text-input-border(v-show='focused', transition='input-border')
</template>
<script>
import './styles/common.less'
import './styles/transition.less'
import './styles/colorloop.less'
export default {
  props: {
    content: {
      twoWay: true
    },
    contentType: {
      type: String,
      default: 'text'
    },
    label: {
      type: String
    }
  },
  data () {
    return {
      focused: false
    }
  },
  computed: {
    hasContent () {
      return this.content && this.content.length > 0
    },
    labelShrink () {
      return this.hasContent || this.focused
    }
  },
  methods: {
    getFocus (e) {
      if (this.focused) {
        return
      }
      this.focused = true
      let input = e.target.nextSibling
      input.focus()
    },
    lostFocus () {
      if (this.model && this.model.length > 0) {
        return
      }
      this.focused = false
    }
  }
}
</script>
