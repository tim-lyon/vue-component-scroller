# vue-component-scroller
A virtual scroller for rendering (very) long lists of vue components.

## Live demo
<https://tim-lyon.github.io/vue-component-scroller/>

## Usage
The package exports a vue component which takes three props: 'item' which is a component that you want to render in the list, 'itemCount' is the length of the list and 'itemHeight' is the fixed height (in pixles) that the components will be rendered at. The 'item' component will be passed a prop 'index' for every instance in the list.

```
<template>
  <div id="app">
	<component-scroller
	  :item="MyComponent"
	  :itemCount="1000000"
	  :itemHeight="60"
	  style="height:400px;"/>
  </div>
</template>

<script>
import ComponentScroller from 'vue-component-scroller'
import MyComponent from './components/MyComponent.vue'

export default {
  components: {
	ComponentScroller
  },
  data() {
    return {
	  MyComponent
    }
  }
}
</script>
```

## Project setup
```
npm install
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
