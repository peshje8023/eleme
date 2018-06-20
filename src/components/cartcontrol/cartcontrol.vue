<template>
	<div class="cartcontrol">
		<transition name="move">
			<div class="cart-decrease" v-show="food.count>0" @click="decreaseCart($event)">
				<span class="inner icon-remove_circle_outline"></span>
			</div>
		</transition>
		<transition name="move">
			<div class="cart-count" v-show="food.count>0">{{food.count}}</div>
		</transition>
		<div class="cart-add icon-add_circle" @click="addCart($event)"></div>
	</div>
</template>

<script type="text/ecmascript-6">
	import Vue from 'Vue' 
	
	export default {
		props: {
			food: {
				type: Object
			}
		},
		mounted(){
			this.$set(this.food,'count',0)
		},
		methods:{
			addCart(event) {
				if(!event._constructed){
					return;
				}
				this.food.count++;
			},
			decreaseCart(event) {
				if(!event._constructed){
					return;
				}
				this.food.count--;
			}
		}
	};
</script>

<style lang="stylus" rel="stylesheet/stylus">
	.cartcontrol
		font-size: 0
		.cart-decrease
			display: inline-block
			padding: 6px
			&.move-enter-active,&.move-leave-active
				transition: all 0.2s linear
				.inner
					transition: all 0.2s linear
			.inner
				display: inline-block
				font-size: 24px
				line-height:24px
				color: rgb(0,160,220)
				transform: rotate(0)
			&.move-enter,&.move-leave-to
				opacity: 0
				transform: translate3D(24px,0,0) 
				.inner
					transform: rotate(180deg)
		.cart-count
			display:inline-block
			vertical-align: top
			width: 12px
			padding-top: 6px
			line-height: 24px
			text-align: center
			font-size: 10px
			color: rgb(147,153,159)
			&.move-enter-active,&.move-leave-active
				transition: all 0.2s linear
			&.move-enter,&.move-leave-to
				opacity: 0
		.cart-add
			display: inline-block
			font-size: 24px
			line-height:24px
			padding: 6px
			color: rgb(0,160,220)
</style>