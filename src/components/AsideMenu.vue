<style lang='less'>
@import './styles/color.less';
.aside-menu{
  width: 100%;
  position: relative;
  height: 3em;
  line-height: 3em;
  padding: 0 1em;
  cursor: pointer;
  display: block;
  .mixin-color-hover;
  .mixin-color-focus;
  a{
    display: inline-block;
    width: 100%;
    color: inherit;
    text-decoration: none;
    &:hover, &:visited{
      color: inherit;
      text-decoration: none;
    }
  }

  > .iconfont{
    float: right;
    margin-left: 20px;
    transition: ease all .2s;
    pointer-events: none;
  }
  .aside-menu-open{
    &.iconfont{
      transform: rotate(180deg);
    }
  }
}
</style>

<template lang='jade'>
div.aside-menu.waves-effect.waves-ripple(:class='{"color-focus": showSubMenu}')
  a(v-if='link && !hasSubMenu', :href='link')
    slot
  slot(v-else)
  span.iconfont(v-if='hasSubMenu', :class='{"aside-menu-open": showSubMenu}') &#xe604;
</template>

<script>
import './waves/waves.less'
export default {
  props: {
    hasSubMenu: {
      type: Boolean,
      default: false
    },
    link: {
      type: String,
      default: ''
    },
    showSubMenu: {
      type: Boolean,
      default: false
    }
  },
  methods: {
  }
}
</script>
