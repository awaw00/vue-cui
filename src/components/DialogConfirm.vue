<style lang='less'>
.dialog-confirm{
  .dialog-body{
    min-width: 200px;
  }
  .dialog-confirm-title{
    display: block;
    font-size: 1.3em;
    padding: 0 0 2px 0;
    margin-bottom: 20px;
    border-bottom: 1px solid #FFFFFF;
  }
  .dialog-confirm-btns{
    padding-top: 10px;
    white-space: nowrap;
    > *{
      float: right;
      &:not(:first-child){
        margin-right: 10px;
      }
    }
  }
}
</style>
<template lang='jade'>
dialog.dialog-confirm(:show='show')
  span.dialog-confirm-title {{title}}
  slot
  p.dialog-confirm-btns
    wave-button(v-if='hasOk', :btn-type='["primary", "raised"]', @btn-click='okClick')
      {{okText}}
    wave-button(v-if='hasCancel', @btn-click='cancelClick')
      {{cancelText}}
</template>
<script>
import './styles/common.less'
import './styles/transition.less'
import './styles/colorloop.less'
import dialog from './Dialog'
import waveButton from './WaveButton'
export default {
  components: {
    'dialog': dialog,
    'wave-button': waveButton
  },
  props: {
    title: {
      type: String,
      default: '确认操作'
    },
    okText: {
      type: String,
      default: '确定'
    },
    cancelText: {
      type: String,
      default: '取消'
    },
    show: {
      type: Boolean,
      default: false,
      twoWay: true
    },
    btns: {
      type: Array,
      default: () => ['ok', 'cancel']
    }
  },
  computed: {
    hasOk () {
      if (!this.btns) { return false }
      for (let i = 0; i < this.btns.length; i++) {
        if (this.btns[i] === 'ok') {
          return true
        }
      }
      return false
    },
    hasCancel () {
      if (!this.btns) { return false }
      for (let i = 0; i < this.btns.length; i++) {
        if (this.btns[i] === 'cancel') {
          return true
        }
      }
      return false
    }
  },
  methods: {
    okClick () {
      this.$dispatch('dialog-confirm-ok')
      this.show = false
    },
    cancelClick () {
      this.$dispatch('dialog-confirm-cancel')
      this.show = false
    }
  }
}
</script>
