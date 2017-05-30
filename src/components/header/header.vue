<template>
	<div class="header">
		<img class="avatar" :src="seller.avatar">
		<div class="sname"><span>品牌</span>{{ seller.name }}</div>
		<p class="description"><span>{{ seller.description }}</span><span>/{{ seller.deliveryTime }}分钟送达</span></p>
		<div class="supports"></div><div class="more_supports">{{seller.supports.length}}个</div>
		<div class="bulletin"><span></span>{{ seller.bulletin }}</div>
	</div>
</template>

<script type='text/ecmascript-6'>
	export default {
        props: {
            seller: {
                type: Object
            }
        }
	};
</script>

<style>
	.header{
		width:100%;
		/* height: 50px; */
		background: grey;
	}
	.avatar{
		margin: 24px 0 0 24px;
		width: 64px;
		height: 64px;
	}
	.sname{
		font-size: 16px;
		color: #fff;
		line-height: 18px;
		font-weight: bold;
	}
	.sname span{
		width: 16px;
		height: 32px;
		color: #fff;
		background-color: red;
		font-size: 12px;
		line-height: 32px;
		text-align: center;
	}
	.description{
		font-size: 12px;
		line-height: 12px;
	}
</style> 
