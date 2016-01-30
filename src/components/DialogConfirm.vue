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
    border-bottom: 1px solid #000000;
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
    span.btn.btn-primary(@click='okClick') {{okText}}
    span.btn.btn-default(@click='cancelClick') {{cancelText}}
</template>
<script>
import './styles/common.less'
import './styles/transition.less'
import './styles/colorloop.less'
import dialog from './Dialog'
export default {
  components: {
    'dialog': dialog
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
