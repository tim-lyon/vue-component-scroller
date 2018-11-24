<template>
  <div :style="{overflowY: 'scroll', outline: 'none'}" @scroll="onScroll" tabindex="1">
    <div :style="{marginTop:topMargin+'px',marginBottom:bottomMargin+'px',}">	
      <component v-for="itemIndex in visibleItems"
		:style="{height:itemHeight+'px',overflow: 'hidden'}"
        :is="item"
        :index="itemIndex" 
        :key="itemIndex"/>
	</div>
  </div>
</template>

<script>

export default {
  name: 'ScrollingDiv',
  props: {
    itemHeight: Number,
	itemCount: Number,
	item: Object,
	bufferSize: {
      type: Number,
      default: 5
    },
  },
  data() {
	return {
		startItem: 0,
		visibleItemCount: 0,
		topMargin: 0,
		bottomMargin: 0,
		scrollTop: 0
		}
  },
  mounted(){
	this.startItem = -this.bufferSize
	const containerHeight = this.$el.clientHeight
	this.visibleItemCount = Math.floor((containerHeight-2*this.itemHeight)/this.itemHeight)+2*this.bufferSize
	const visibleHeight = this.itemHeight*this.visibleItemCount
	const realTotalHeight = this.itemHeight*this.itemCount
	const totalHeight = Math.min(realTotalHeight,10e6)
	this.totalMargin = totalHeight - visibleHeight
	this.marginFactor = (realTotalHeight-visibleHeight)/(this.totalMargin)
	this.maxScrollTop = Math.max(0, totalHeight - containerHeight)
	this.maxStartItem = Math.max(0, this.itemCount - this.visibleItemCount)
	this.topMargin = 0
	this.bottomMargin = this.totalMargin
  },
  watch: {
	startItem(){
		this.topMargin = Math.max(0,Math.floor(this.itemHeight*this.startItem/this.marginFactor))
		this.bottomMargin = this.totalMargin - this.topMargin
	},
	scrollTop(){
		this.startItem = Math.ceil(this.scrollTop*this.marginFactor/this.itemHeight)-this.bufferSize
		this.startItem = Math.min(this.startItem, this.maxStartItem)
		this.startItem = Math.max(this.startItem, -this.bufferSize)
	}
  },
  computed: {
	visibleItems(){
		let visibleItems = []
		for(var i=0; i<=this.visibleItemCount; ++i){
			if(this.startItem + i>0 && this.startItem + i<=this.itemCount){
				visibleItems.push(this.startItem + i)
			}
		}
		return visibleItems
	}
  },
  methods: {
	onScroll(){
		this.scrollTop = this.$el.scrollTop
	}
  }
}
</script>