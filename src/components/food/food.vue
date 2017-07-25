<template>
	<div class="food">
		<span class="back" v-on:click="back"></span>
        <div class="head_pic_wrap">
            <img v-bind:src="food.image" alt="">
        </div>
        <div class="info">
            <p class="food_name">{{ food.name }}</p>
            <p class="food_sell_rating">
                <span>月售{{ food.sellCount }}份</span>
                <span>好评率{{ food.rating }}%</span>
            </p>
            <p class="food_price">
                <span><i>￥</i><i>{{ food.price }}</i></span>
                <span v-if="food.oldPrice">￥{{ food.oldPrice }}</span>
            </p>
            <div class="food_add_shopcart">加入购物车</div>
        </div>
	</div>
</template>

<script type='text/ecmascript-6'>
    export default {
        props: {
            food: {
                type: Object
            }
        },
        methods: {
            back () {
                this.$emit('backTo');
            }
        }
    };
</script>

<style>
	.food{
        width:100%;
        height:100%;
        background:#fff;
        position:fixed;
        top:0;
        left:0;
        bottom:54px;
    }
    .back{
        display: block;
        width:15px;
        height:32px;
        color:#fff;
        background:url(./images/back.png) no-repeat center center;
        background-size: 15px 32px;
        position: absolute;
        left:20px;
        top:20px;
        z-index:999;
    }
    .head_pic_wrap{
        width:100%;
        padding-top:100%;
    }
    .head_pic_wrap img{
        position:absolute;
        left:0;
        top:0;
        width:100%;
    }
    .food .info{
        height:60px;
        padding:10px 18px;
    }

    .info .food_name{
        font-size:20px;
        font-weight:bold;
        line-height: 36px;
        height: 36px;
    }
    .info .food_sell_rating{
        font-size:16px;
        color:grey;
    }
    .info .food_sell_rating span{
        display: inline-block;
        height: 20px;
        line-height:20px;
        margin-right: 10px;
    }

    .info .food_price{

    }
    .info .food_price span:first-child{

    }
    .info .food_price span:first-child i:first-child{
        font-size:12px;
    }
    .info .food_price span:first-child i:last-child{
        font-size:20px;
    }
    .info .food_price span:last-child{

    }




    .info .food_add_shopcart{

    }
</style>
