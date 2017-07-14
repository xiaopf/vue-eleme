<template>
	<div class="tab">
        <div class="tab-item"><router-link to="/goods">商品</router-link></div>
        <div class="tab-item"><router-link to="/ratings">评论</router-link></div>
        <div class="tab-item"><router-link to="/seller">商家</router-link></div>
	</div>
</template>

<script type='text/ecmascript-6'>
	export default {};
</script>

<style>
	.tab{
        display: flex;
        width: 100%;
        height: 40px;
        line-height: 40px;
        border-bottom:1px solid grey;
	}
	.tab-item{
		flex: auto;
		text-align: center;
	}
	.tab-item a{
		display: block;
		height: 100%;
		width: 100%;
		font-size: 14px;
		color:#000;
	}
	.tab-item .router-link-active {
		color:red;
	}
</style> 
