<template>
	<div class="shopcart">
		<div class="content">
			<div class="content-left">
				<div class="logo-wrapper">
					<div class="logo" :class="{highlight:totalCount>0}">
						<i class="icon-shopping_cart" :class="{highlight:totalCount>0}"></i>
					</div>
					<div class="num" :class="{highlight:totalCount>0}">{{totalCount}}</div>
				</div>
				<div class="price" :class="{highlight:totalCount>0}">￥{{totalPrice}}</div>
				<div class="desc">另需配送费{{deliveryPrice}}元</div>
			</div>
			<div class="content-right" :class="{highlight:totalPrice >= minPrice}">
				<div class="pay">{{payDesc}}</div>
			</div>
		</div>
		<div class="ball-container"></div>
		
	</div>
</template>

<script type="text/ecmascript-6">
	import cartcontrol from 'components/cartcontrol/cartcontrol'
	
	export default {
		props:{
			deliveryPrice: {
				type: Number,
				default: 0
			},
			minPrice: {
				type: Number,
				default: 0
			},
			selectFoods: {
				type: Array,
				default() {
					return []
				}
			}
		},
		data() {
			return {
				balls: [
					{
						show: false
					},
					{
						show: false
					},
					{
						show: false
					},
					{
						show: false
					},
					{
						show: false
					}
				],
			}
		},
		computed: {
			totalPrice() {
				let total = 0;
				this.selectFoods.forEach((food) => {
					total += food.price * food.count;
				});
				return total;
			},
			totalCount() {
				let count = 0;
				this.selectFoods.forEach((food) => {
					count += food.count;
				});
				return count;
			},
			payDesc() {
				if(this.totalPrice === 0){
					return `￥${this.minPrice}元起送`;
				}
				else if(this.totalPrice < this.minPrice) {
					let diff = this.minPrice - this.totalPrice
					return `还差￥${diff}元起送`
				}
				else{
					return '去结算';
				}
			},
			listShow() {
				if(!this.totalCount) {
					this.fold = true;
					return false;
				}
				let show = !this.fold;
				return true;
			}
		},
		components:{cartcontrol},
	};
</script>

<style lang="stylus" rel="stylesheet/stylus">
	.shopcart
		position: fixed
		bottom: 0
		left: 0
		z-index: 50
		width: 100%
		height: 48px
		.content
			display: flex
			background: #141d27
			font-size: 0
			color: rgba(255,255,255,0.4)		
			.content-left
				flex: 1
				.logo-wrapper
					vertical-align: top
					display: inline-block
					position: relative
					top: -10px
					margin: 0 12px
					padding: 6px
					width: 56px
					height: 56px
					box-sizing: border-box
					border-radius: 50%
					background: #141d27
					.logo
						width: 100%
						height: 100%
						border-radius: 50%
						background: #2b343c
						text-align: center
						&.highlight
							background: rgb(0,160,220)
						.icon-shopping_cart
							line-height: 44px
							color: #80858a
							font-size: 24px
							&.highlight
								color: #fff
					.num
						display: none
						position: absolute
						top: 0
						right: 0
						width: 24px
						height: 16px
						line-height: 16px
						text-align: center
						border-radius: 16px
						font-size: 9px
						font-weight: 700
						color: #fff
						background-color: rgb(240,20,20)
						box-shadow: 0 4px 8px 0 rgba(0,0,0,0.4)
						&.highlight
							display: block
				.price
					display: inline-block
					vertical-align: top
					margin-top: 12px
					line-height: 24px
					padding-right: 12px
					box-sizing: border-box
					border-right: 1px solid rgba(255,255,255,0.1)
					font-size: 16px
					font-weight: 700
					&.highlight
						color: #fff
				.desc
					display: inline-block
					vertical-align: top
					margin-left: 12px
					line-height: 48px
					font-size: 10px					
			.content-right
				flex: 0 0 105px
				width: 105px
				background: #2b343c
				&.highlight
					background: green
					.pay
						color: #fff
				.pay
					height: 48px
					line-height: 48px
					text-align: center
					font-size: 12px
					font-weight: 700
					
				
</style>