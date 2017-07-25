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
                <span class="food_price_new"><i>￥</i><i>{{ food.price }}</i></span>
                <span class="food_price_old" v-if="food.oldPrice">￥{{ food.oldPrice }}</span>
            </p>
            <div class="food_add_shopcart">加入购物车</div>
            <vshopBtn v-if=false></vshopBtn>
        </div>
        <div v-if="food.info" class="line_grey"></div>
        <div v-if="food.info" class="info_detail">
            <h2>商品介绍</h2>
            <p>{{ food.info }}</p>
        </div>
        <div class="line_grey"></div>
	</div>
</template>

<script type='text/ecmascript-6'>
    import shopBtn from '../shopBtn/shopBtn';
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
        },
        components: {
            vshopBtn: shopBtn
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
        height:auto;
        padding:6px 18px 18px;
        position: relative;
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
        padding-top: 10px;
        height: 20px;
    }
    .info .food_price .food_price_new{
 
    }
    .info .food_price .food_price_new i:first-child{
        font-size:14px;
        font-style: normal;
        font-weight: bold;
        color:red;
    }
    .info .food_price .food_price_new i:last-child{
        font-size:20px;
        font-style: normal;
        font-weight: bold;
        color:red;
    }
    .info .food_price .food_price_old{
        margin-left:10px;
        font-size:18px;
        color:grey;
    }
    .info .food_add_shopcart{
        position: absolute;
        right: 18px;
        bottom:18px;
        width:104px;
        height:36px;
        border-radius:14px;
        background-color:#008fe1;
        line-height:36px;
        text-align:center;
        font-size:18px;
        color:#fff;
    }
    .line_grey{
        width: 100%;
        height:20px;
        background-color:#f3f5f7;
    }
    .info_detail{
        padding:18px;
    }
    .info_detail h2{
        font-size:20px;
        line-height: 20px;
        height:20px;
    }
    .info_detail p{
        font-size:16px;
        line-height: 24px;
        color:grey;
    }
</style>
