<template>
	<div class="shopcart">
        <div class="car_icon"><span class="icon"></span></div>
        <div class="total_price">￥40</div>
        <div class="send_price">另需配送费￥4元</div>
        <div class="order_msg">￥10起送</div>
	</div>
</template>

<script type='text/ecmascript-6'>
	export default {
	};
</script>
<style>
.shopcart{
    width: 100%;
    height: 54px;
    background-color: #111b26;
    position: absolute;
    bottom: 0;
    left: 0;
    font-size: 0;
}
.car_icon{
    display: inline-block;
    width: 66px;
    height: 66px;
    position: absolute;
    left: 10px;
    bottom: 4px;
    background-color: #111b26;
    border-radius: 50%;
}
.icon{
    display: inline-block;
    width: 50px;
    height: 50px;
    background: url(./images/car.png) no-repeat 9px 12px;
    background-size: 30px 28px;
    background-color: #27343e;
    margin: 8px 0 0 8px;
    border-radius: 50%;
}
.icon_blue{
    background: url(./images/car_white.png) no-repeat center center;
    background-color: #008fe1;
}
.total_price{
    display: inline-block;
    width: auto;
    margin-top: 9px;
    padding: 0 8px;
    height: 36px;
    margin-left: 74px;
    font-size: 20px;
    line-height: 36px;
    font-weight: bold;
    color: #fff;
    border-right: 2px solid #232e38;
}
.send_price{
    display: inline-block;
    font-size: 16px;
    color: #90949d;
    padding: 0 4px;
}
.order_msg{
    display: inline-block;
    float: right;
    background-color: #28323b;
    font-size: 18px;
    font-weight: bold;
    text-align: center;
    line-height: 54px;
    color: #90949d;
    width: 24%;
    height: 54px;
}
</style>
