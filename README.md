# Brace

Code editor powered by Vuejs and browserify Ace (Brace)

## Installation

```
$ npm install vue-bulma-brace --save
```


## Examples

```vue
<template>
  <div>
    <brace style="height: 500px" 
      :fontsize="'12px'" 
      :theme="'github'" 
      :mode="'json'"
      :codefolding="'markbegin'"
      :softwrap="'free'"
      :selectionstyle="'text'"
      :highlightline="true"
      @code-change="codeChange"
      ref="editor">
    </brace>
  </div>
</template>

<script>
import Brace from 'vue-bulma-brace'

export default {
  components: {
    Brace
  },
  mounted () {
    // Set the initial value
    this.$refs.editor.setCode("// the initial value")
  },
  methods: {
    codeChange (newValue) {
      // Use the value
    }
  }
}
</script>
```


## Badges

![](https://img.shields.io/badge/license-MIT-blue.svg)
![](https://img.shields.io/badge/status-dev-yellow.svg)

---
