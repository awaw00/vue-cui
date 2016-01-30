<style lang='less'>
@import './components/styles/color.less';
#app{
  margin: 0 auto;
  width: 666px;
  .logo{
    text-align: center;
    padding: 30px;
  }
  .color-selections{
    cursor: pointer;
    margin: 20px 0;
    > div{
      width: 30px;
      height: 30px;
      display: inline-block;
      outline-offset: 1px;
    }
  }
  .wave-buttons{
    .wave-button{
      &:not(:last-child){
        margin-right: 10px;
      }
    }
  }
}
.loopper(@counter) when (@counter > 0){
  .loopper((@counter - 1));
  .color-selections{
    .theme-@{counter}{
      .color-normal(@counter);
    }
  }
}
.loopper(@color-count);
</style>

<template lang='jade'>
div#app(:class='[themeStyle]')
  div.logo.color-normal
    img(src='./assets/logo.png')
    h1 vue-cui
    h2 colorful ui components for vue.js
  div.color-selections
    div(v-for='t in themes', :class='"theme-" + t', @click='theme = t')
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
export default {
  components: {
    textInput,
    selectInput,
    progressBar,
    waveButton,
    dialogConfirm
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
