<style lang='less'>
@import './styles/color.less';
.aside-container{
  width: 260px;
  &.aside-left{
    float: left;
    box-shadow: 1px 0 10px 1px rgba(0, 0, 0, 0.31);
  }
  &.aside-right{
    float: right;
    box-shadow: -1px 0 10px 1px rgba(0, 0, 0, 0.31);
  }
  &.aside-fixed{
    position: fixed;
    top: 0;
    bottom: 0;
    float: none;
    &.aside-left{
      left: 0;
    }
    &.aside-right{
      right: 0;
    }
  }
  .aside-main{
    width: 100%;
    height: 100%;
  }
  .aside-menus{
    overflow-y: auto;
    .aside-sub-menus{
      .aside-menu{
        padding-left: 2em;
      }
    }
  }
  .aside-footer{
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
  }
}
</style>

<template lang='jade'>
div.aside-container(:class='asideStyle')
  div.aside-mask
  div.aside-main.color-normal
    div.aside-header
      slot(name='header')
    div.aside-menus
      template(v-for='menu in menus')
        aside-menu(:has-sub-menu='hasSubMenu(menu)', :link='menuLink(menu)', @click='mainMenuClick(menu)', :show-sub-menu='showSubMenu(menu)')
          {{{menu.content}}}
        div.aside-sub-menus(v-show='showSubMenu(menu)', transition='menu')
          aside-menu(v-for='subMenu in menu.subMenus', :link='menuLink(subMenu)')
            {{{subMenu.content}}}
    div.aside-footer
      slot(name='footer')
</template>

<script>
import asideMenu from './AsideMenu'
export default {
  components: {
    'aside-menu': asideMenu
  },
  props: {
    asideType: {
      type: Array,
      default: () => ['left', 'fixed']
    },
    menus: {
      type: Array,
      default: () => []
    }
  },
  data () {
    return {
      currentMenu: null
    }
  },
  computed: {
    asideStyle () {
      return this.asideType.map((item) => item = 'aside-' + item)
    }
  },
  methods: {
    mainMenuClick (menu) {
      if (this.hasSubMenu(menu)) {
        if (menu === this.currentMenu) {
          menu.showSubMenu = !menu.showSubMenu
        } else {
          if (this.currentMenu) { this.currentMenu.showSubMenu = false }
          this.currentMenu = menu
          this.currentMenu.showSubMenu = true
        }
      }
    },
    hasSubMenu (menu) {
      if (menu.subMenus && menu.subMenus.length > 0) {
        return true
      }
      return false
    },
    showSubMenu (menu) {
      return this.hasSubMenu(menu) && menu.showSubMenu === true
    },
    menuLink (menu) {
      if (menu.link) {
        return menu.link
      }
      return ''
    }
  },
  created () {
    for(let i = 0; i < this.menus.length; i++) {
      if (this.menus[i].showSubMenu === undefined) {
        this.menus[i] = {...this.menus[i], showSubMenu: false}
      }
    }
  }
}
</script>
