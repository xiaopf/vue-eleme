<template>
	<div class="shopcart">
        <div v-if="shopcartDetail && totalL" class="shopcartDetailShade" v-on:click="clickShade"></div>
        <div v-if="shopcartDetail && totalL" class="shopcart_detail">
            <div class="shopcart_title">
                <p class="shopcart_title_text">购物车</p>
                <p class="shopcart_title_clearAll" v-on:click="clearAllItems">清空</p>
            </div>
            <ul>
                <li v-for="(item,key) in pitchFoodsShopcart"  v-if="item[0]"  class="food_item">
                    <span class="shopcart_name">{{ item[1].name }}</span>
                    <!-- <span v-if="item[1].description" class="shopcart_description">({{ item[1].description }})</span> -->
                    <vShopBtn v-on:clickPlus="clickPlus(item[1].name,item[1].price)" v-on:clickReduce="clickReduce(item[1].name,item[1].price)" v-bind:itemNum="item[0]"></vShopBtn>
                    <span class="shopcart_price">￥{{ item[1].price * item[0] }}</span>
                    <span v-if="item[1].oldPrice" class="shopcart_oldPrice">￥{{ item[1].oldPrice }}</span>
                </li>
            </ul>
        </div>
        <div class="car_icon"><span v-on:click="showDetail"  class="icon" v-bind:class="{icon_blue:totalL}"><span v-if="totalL" class="icon_ttNums">{{totalL}}</span></span></div>
        <div class="total_price">￥{{totalPriceL}}</div>
        <div class="delivery_price">另需配送费￥{{deliveryPrice}}元</div>
        <div class="order_msg" v-bind:class="{order_msg_green:!showMinPrice}">
            <span v-if="showMinPrice">
                <span v-if="totalPriceL">还差</span><span>￥{{  shortPrice }}</span>
                <span>起送</span>
            </span>
            <span v-else class="calculate" v-on:click="countAll">结算</span>
        </div>
	</div>
</template>

<script type='text/ecmascript-6'>
    import shopBtn from '../shopBtn/shopBtn.vue';
	export default {
        props: {
            total: Number,
            totalPrice: Number,
            minPrice: Number,
            deliveryPrice: Number,
            shopcartD: Boolean,
            pitchFoods: {
                type: Object
            }
        },
        data () {
            return {
                shortPrice: this.minPrice,
                shopcartDetail: this.shopcartD,
                totalL: this.total,
                totalPriceL: this.totalPrice,
                pitchFoodsShopcart: this.pitchFoods
            };
        },
        watch: {
            total (val) {
                this.totalL = val;
            },
            totalPrice (val) {
                this.totalPriceL = val;
            },
            pitchFoods (val) {
                this.pitchFoodsShopcart = val;
            },
            shopcartD (val) {
                this.shopcartDetail = val;
            }
        },
        computed: {
            showMinPrice () {
                if (this.totalPriceL < this.minPrice) {
                    this.shortPrice = this.minPrice - this.totalPriceL;
                    return true;
                } else {
                    return false;
                }
            }
        },
        methods: {
            showDetail () {
                if (this.total > 0) {
                    if (this.shopcartDetail) {
                       this.shopcartDetail = false;
                    } else {
                       this.shopcartDetail = true;
                    };
                }
            },
            clickPlus (n, p) {
                this.$emit('clickPlusShop', n, p);
            },
            clickReduce (n, p) {
                this.$emit('clickReduceShop', n, p);
                if (this.totalL === 1) {
                    this.shopcartDetail = false;
                };
            },
            clearAllItems () {
                this.pitchFoodsShopcart = {};
                this.shopcartDetail = false;
                this.totalPriceL = 0;
                this.totalL = 0;
                this.$emit('clearAll');
            },
            clickShade () {
                if (this.total > 0) {
                    if (this.shopcartDetail) {
                       this.shopcartDetail = false;
                    } else {
                       this.shopcartDetail = true;
                    };
                }
            },
            countAll () {
                console.log();
            }
        },
        components: {
            vShopBtn: shopBtn
        }
	};
</script>
<style>
.shopcart{
    width: 100%;
    height: 54px;
    background-color: #111b26;
    position: absolute;
    bottom: 0px;
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
    z-index:999;
    display: inline-block;
    width: 50px;
    height: 50px;
    background: url(./images/car.png) no-repeat 9px 12px;
    background-size: 30px 28px;
    background-color: #27343e;
    margin: 8px 0 0 8px;
    border-radius: 50%;
}
.icon_ttNums{
    z-index:999;
    display: inline-block;
    width: auto;
    padding: 0 10px;
    height: 22px;
    border-radius: 10px;
    background-color: #ff3904;
    font-size: 16px;
    line-height: 22px;
    color: #fff;
    text-align: center;
    position: absolute;
    left:40px;
    top:2px;

}
.icon_blue{
    background: url(./images/car_white.png) no-repeat 9px 12px;
    background-size: 30px 28px;
    background-color: #008fe1;
}
.total_price{
    display: inline-block;
    width: auto;
    margin-top: 9px;
    padding: 0 8px;
    height: 36px;
    margin-left: 74px;
    font-size: 16px;
    line-height: 36px;
    font-weight: bold;
    color: #fff;
    border-right: 2px solid #232e38;
}
.delivery_price{
    display: inline-block;
    font-size: 12px;
    color: #90949d;
    padding: 0 4px;
}
.order_msg{
    display: inline-block;
    position: absolute;
    right:0;
    top:0;
    background-color: #28323b;
    font-size: 14px;
    font-weight: bold;
    text-align: center;
    line-height: 54px;
    color: #90949d;
    width: auto;
    height: 54px;
    padding:0 10px;
}
.order_msg span{
    line-height: 30px;
    height: 30px;
    display: inline-block;
}
.order_msg_green{
    background-color: #25bb64;
    color: #fff;
}
.shopcart_detail::-webkit-scrollbar{
    display: none;
}
.shopcart_detail{
    position: absolute;
    bottom:54px;
    left:0;
    width: 100%;
    max-height: 764%;
    height: auto;
    overflow: auto;
    background-color: #fff;
    padding: 0 0 24px 0;
}
.shopcart_title{
    width: 100%;
    height: 40px;
    background-color: #f3f5f7;
    font-size: 0;
}
.shopcart_title_text{
    display: inline-block;
    float: left;
    color: #07111b;
    height: 40px;
    font-size: 18px;
    line-height: 40px;
    padding: 0 20px;
}
.shopcart_title_clearAll{
    display: inline-block;
    float: right;
    color: #008fe1;
    height: 40px;
    font-size: 16px;
    line-height: 40px;
    padding: 0 20px;
}
.calculate{
    display: inline-block;
    width:3em;
    font-size: 18px;
}
.food_item{
    width:92%;
    height: 50px;
    margin: 0 4%;
    border-bottom:1px solid grey;
    line-height: 50px;
    font-size: 0;
}
.food_item>span{
    line-height: 50px;
}
.food_item .shopBtn{
    padding-top: 12px;
}
.shopcart_name{
    font-size: 16px;
    font-weight: bold;
    color:#000;
}
.shopcart_description{
    font-size: 14px;
    color:grey;
    width: 6em;
    padding: 0 10px;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
}
.shopcart_oldPrice{
    font-size: 14px;
    color:grey;
    float:right;
    text-decoration: line-through;
}
.shopcart_price{
    font-size: 16px;
    font-weight: bold;
    color:red;
    float:right;
    padding: 0 16px 0 4px;
}
.shopcartDetailShade{
    width: 100% ;
    height: 100%;
    position:fixed;
    top:0;
    left:0;
    background-color: rgba(0,0,0,0.5);
}

</style>
