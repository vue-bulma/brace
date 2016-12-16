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
      :highlightline="true">
    </brace>
  </div>
</template>

<script>
import Brace from 'vue-bulma-brace'

export default {
  components: {
    Brace
  }
}
</script>
```


## Badges

![](https://img.shields.io/badge/license-MIT-blue.svg)
![](https://img.shields.io/badge/status-dev-yellow.svg)

---
