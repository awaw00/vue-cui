<style lang='less'>
@import './components/styles/color.less';
body{
  margin: 0;
  padding: 0;
}
#app{
  margin-left: 265px;
  width: 666px;
  .aside-container{
    max-width: 260px;
    .aside-main{
      transition: ease background-color .6s;
    }
    .aside-menus{
      box-shadow: 0px -5px 10px -4px rgba(0, 0, 0, 0.5);
      position: absolute;
      top: 382px;
      left: 0;
      right: 0;
      bottom: 90px;
    }
    .aside-footer{
      padding: 10px;
    }
  }
  .logo{
    text-align: center;
    padding: 30px;
    img{
      width: 160px;
    }
    p{
      font-size: 16px;
    }
  }
  .pallettes{
    cursor: pointer;
    > div{
      width: 30px;
      height: 30px;
      display: inline-block;
      border: 1px solid #FFFFFF;
    }
  }
  .wave-buttons{
    .wave-button{
      &:not(:last-child){
        margin-right: 10px;
      }
    }
  }
  .content{
    padding: 10px;
  }
}
.loopper(@counter) when (@counter > 0){
  .loopper((@counter - 1));
  .pallettes{
    .theme-@{counter}{
      .color-normal(@counter);
    }
  }
}
.loopper(@color-count);
</style>

<template lang='jade'>
div#app(:class='[themeStyle]')
  aside(:aside-type='["left", "fixed"]', :menus='aside.menus')
    div.logo.color-normal(slot='header')
      img(src='./assets/logo.png')
      h1 vue-cui
      p Colorful UI Components
      p For Vue.js
    div.pallettes(slot='footer')
      div(v-for='t in themes', :class='"theme-" + t', @click='theme = t')
  div.content
    text-input(:label='textInput.label', :value.sync='textInput.value', content-type='password')
    br
    select-input(:label='selectInput.label', :value.sync='selectInput.value', :key.sync='selectInput.key', :options='selectInput.options')
    br
    progress-bar(:percentage='progressBar.percentage')
    br
    div.wave-buttons
      wave-button
        span Default
      wave-button(:btn-type='["raised", "primary"]')
        span Primary
      wave-button(:btn-type='["raised", "accent"]', @btn-click='dialogConfirm.show = true')
        span Accent
      wave-button(:btn-type='["raised", "primary", "sharp"]')
        span Sharp
    dialog-confirm(:show.sync='dialogConfirm.show', :btns='["ok"]')
      {{dialogConfirm.content}}
</template>

<script>
import textInput from './components/TextInput'
import selectInput from './components/SelectInput'
import progressBar from './components/ProgressBar'
import waveButton from './components/WaveButton'
import dialogConfirm from './components/DialogConfirm'
import aside from './components/Aside'
export default {
  components: {
    textInput,
    selectInput,
    progressBar,
    waveButton,
    dialogConfirm,
    aside
  },
  data () {
    return {
      textInput: {
        label: 'Text Input',
        value: ''
      },
      selectInput: {
        label: 'Select Input',
        options: [
          { key: 1, value: 'this is option 1' },
          { key: 3, value: 'this is option 2' },
          { key: 5, value: 'this is option 3' }
        ],
        key: null,
        value: null
      },
      progressBar: {
        percentage: 0
      },
      themes: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16],
      theme: 1,
      dialogConfirm: {
        show: false,
        content: '删除后无法恢复，确定要删除该项目吗？'
      },
      aside: {
        menus: [
          { content: 'Home', link: '#' },
          { content: 'Components', subMenus: [
            { content: 'Aside', link: '#Aside'},
            { content: 'Dialog', link: '#Dialog' },
            { content: 'Dialog Confirm', link: '#DialogConfirm' },
            { content: 'Drawer', link: '#Drawer' },
            { content: 'Progress Bar', link: '#ProgressBar' },
            { content: 'Select Input', link: '#SelectInput' },
            { content: 'Text Input', link: '#TextInput' },
            { content: 'Wave Button', link: '#WaveButton' },
          ] },
          { content: 'Colors', link: '#Colors' }
        ]
      }
    }
  },
  computed: {
    themeStyle () {
      return 'color-' + this.theme
    }
  },
  created () {
    setInterval(() => this.progressBar.percentage = (this.progressBar.percentage + 10) % 110, 1000)
  }
}
</script>
