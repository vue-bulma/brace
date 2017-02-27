<template>
  <div id='vue-bulma-editor'></div>
</template>

<script>
import * as brace from 'brace'
import 'brace/ext/modelist'
import 'brace/ext/themelist'

const modelist = brace.acequire('ace/ext/modelist')
const themelist = brace.acequire('ace/ext/themelist')
var editor

const regMap = {
  isInt: new RegExp('^\\d+$')
}

export default {
  props: {
    mode: {
      type: String,
      default: 'json',
      validator: (val) => modelist.modes.findIndex((mode) => mode.name === val) > -1
    },
    theme: {
      type: String,
      default: 'github',
      validator: (val) => themelist.themes.findIndex((theme) => theme.name === val) > -1
    },
    // todo editor split
    fontsize: {
      type: String,
      default: '12px',
      validator: (val) => parseInt(val) > 11 && parseInt(val) < 25
    },
    codefolding: {
      type: String,
      default: 'markbegin',
      validator: (val) => ['manual', 'markbegin', 'markbeginend'].includes(val)
    },
    // todo key binding
    softwrap: {
      type: String,
      default: 'free',
      validator: (val) => (['off', 'free'].includes(val) || regMap.isInt.test(val))
    },
    selectionstyle: {
      type: String,
      default: 'text',
      validator: (val) => ['text', 'line'].includes(val)
    },
    highlightline: {
      type: Boolean,
      default: true
    }
    // todo a lot of other things...
  },

  methods: {
    setMode () {
      let modeObj = modelist.modesByName[this.mode]

      if (modeObj) {
        require('brace/mode/' + modeObj.name)
        editor.getSession().setMode(modeObj.mode)
      }
    },
    setTheme () {
      let themeObj = themelist.themesByName[this.theme]

      if (themeObj) {
        require('brace/theme/' + themeObj.name)
        editor.setTheme(themeObj.theme)
      }
    },
    emitCode () {
      this.$emit('code-change', editor.getValue())
    }
  },

  mounted () {
    editor = brace.edit('vue-bulma-editor')
    this.setMode()
    this.setTheme()
    editor.$blockScrolling = Infinity
    editor.getSession().on('change', this.emitCode)
  },

  watch: {
    mode () {
      this.setMode()
    },
    theme () {
      this.setTheme()
    },
    fontsize (newVal) {
      editor.setFontSize(newVal)
    },
    codefolding (newVal) {
      editor.session.setFoldStyle(newVal)
      editor.setShowFoldWidgets(newVal !== 'manual')
    },
    softwrap (newVal) {
      editor.setOption('wrap', newVal)
    },
    selectionstyle (newVal) {
      editor.setOption('selectionStyle', newVal)
    },
    highlightline (newVal) {
      editor.setHighlightActiveLine(newVal)
    }
  }
}
</script>
