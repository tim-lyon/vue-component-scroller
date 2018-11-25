# vue-component-scroller
A virtual scroller for rendering (very) long lists of vue components.

[Live demo](https://tim-lyon.github.io/vue-component-scroller/)

## Install
`npm install vue-component-scroller`

## Use
The package exports a vue component which takes three props:
 - `item` is a component that you want to render in the list
 - `itemCount` is the number of components you want in the list
 - `itemHeight` is the fixed height (in pixles) that the components will be rendered at.
 
>Unfortunately, a fixed height for the `item` component is necessary - to pre-calculate the total height of millions of unique components would take too long.

The `item` component is passed a prop `index` for every instance in the list, allowing it to fetch data or render content based on its position in the list. This makes is particularly useful for rending long lists of repetitive data: table rows, contacts, photos etc *without* having to fetch any of the data in advance.

In the code below, the `ComponentScroller` will render a (high performance) scrolling list of 100,000 instances of  `MyComponent`.

```html
<template>
  <div id="app">
    <component-scroller
      :item="MyComponent"
      itemCount="100000"
      itemHeight="60"
      style="height:400px;"/>
  </div>
</template>

<script>
import ComponentScroller from 'vue-component-scroller'
import MyComponent from './components/MyComponent.vue'

export default {
  components: {	ComponentScroller },
  data() {
    return { MyComponent } // MyComponent is in data so it
  }                        // can be passed as a prop!
}
</script>
```
