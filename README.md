# vue-component-scroller
A virtual scroller for rendering (very) long lists of vue components.

[Live demo](https://tim-lyon.github.io/vue-component-scroller/)

## Install
```
npm install vue-component-scroller
```

## Use
The package exports a vue component which takes two props:
 - `itemCount` is the number of items you want in the list
 - `itemHeight` is the fixed height (in pixles) of each item
 
>Unfortunately, a fixed height for each `item` is necessary - to pre-calculate the total height of all the list items would take too long.

Each item is given a slot for adding content. The variable `index` can be used inside the slot, allowing it to fetch data or render content based on its position in the list. This makes it particularly useful for rending long lists of repetitive data: table rows, contacts, photos etc *without* having to fetch any of the data in advance.

In the code below (complete sinlge file component), the `VueComponentScroller` should render a (high performance) scrolling list of 100,000 items.

```html
<template>
  <div id="app">
    <vue-component-scroller class="scroll" :itemCount="100000" :itemHeight="50">
      <div class="item" slot-scope="{index}">
        Item number {{index}}
      </div>
    </vue-component-scroller>
  </div>
</template>

<script>
import VueComponentScroller from 'vue-component-scroller'
export default {
  components: {
    VueComponentScroller
  }
}
</script>

<style>
.scroll {
  height: 300px;
  margin:50px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  border:2px solid red;
}
.item {
  text-align: center;
  height:40px;
  margin:auto 20px;
  box-sizing: border-box;
  box-shadow: 0 3px 6px rgba(0,0,0,.16),0 3px 6px rgba(0,0,0,.23);
}
</style>
```
