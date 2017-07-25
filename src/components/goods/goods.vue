<template>
	<div class="goods">
		<div class="menu_wrap">
			<ul class="menu_wrap_ul">
				<li v-for="(good,index) in goodList" class="good_name" v-on:click="anchor(index)" v-bind:class="{ whiteBg: menuClick[index]}" ref="menuNameTop">
					<span class="text">
						<span v-bind:class="getIconType(good.type)"></span>{{good.name}}
					</span>
				</li>
			</ul>
		</div>
		<div class="food_wrap">
			<ul class="food_wrap_ul" v-on:scroll="scroll_event">
				<li v-for="(good,gIndex) in goodList" class="food_list" ref="foodList">
                     <div v-for="(food,index) in good.foods" class="food_list_item" ref="foodListItem">
                        <vfood v-show="showFoodWrap[index]" v-bind:food="food" v-on:backTo="backTo"></vfood>
                        <h3 v-if="index===0" class="food_title" v-bind:id="foodAnchor(gIndex)" v-bind:class="{food_title_fixed:foodTitleFixed[gIndex]}" ref="foodTitleTop">{{good.name}}</h3>
                        <div class="food_detail" v-on:click="showFood(index,$event)">
                            <div class="food_detail_left">
                            	<img v-bind:src="food.icon" alt="">
                            </div>
                            <div  class="food_detail_right">
                                <p class="food_name">{{food.name}}</p>
                                <p class="des_rat_n">{{food.description}}</p>
                                <p class="des_rat_n">
                                	<span>月售{{food.sellCount}}份</span>
                                 	<span>好评率{{food.rating}}%</span>
                                </p>
                                <p class="price_num_wrap">
	                                <span class="price">
	                                	<span>￥</span><span>{{food.price}}</span>
	                                </span>
                                    <vShopBtn v-if="reRender" v-on:clickPlus="clickPlus(food.price,food)" v-on:clickReduce="clickReduce(food.price,food)" v-bind:itemNum="fakeNumC(food.name)"></vShopBtn>
                                </p>
                            </div>
                        </div>
                     </div>
				</li>
			</ul>
		</div>
        <div class="item_detail_shade">
            <div class="item_detail">
                
            </div>
        </div>
        <vshopcart v-bind:shopcartD="shopcartDetail"  v-bind:total="totalNum"  v-bind:totalPrice="totalP" v-bind:minPrice="minPrice" v-bind:deliveryPrice="deliveryPrice" v-bind:pitchFoods="pitchFoods" v-on:clickPlusShop="clickPlusShop" v-on:clickReduceShop="clickReduceShop" v-on:clearAll="clearAllItems"></vshopcart>
	</div>
</template>

<script type='text/ecmascript-6'>
    import shopBtn from '../shopBtn/shopBtn.vue';
    import shopcart from '../shopcart/shopcart';
    import food from '../food/food';
	export default {
        props: {
            minPrice: Number,
            deliveryPrice: Number
        },
		data () {
            return {
                goodList: [],
                foodTitleTop: [],
                menuClick: [true],
                foodTitleFixed: [false],
                menuNameP: [],
                add: true,
                scrollOnOff: true,
                foodTitleP: [],
                fullIndex: 0,
                overflowH: 0,
                totalNum: 0,
                totalP: 0,
                pitchFoods: {},
                reRender: true,
                shopcartDetail: false,
                scrollEvent: true,
                clicked: true,
                showFoodWrap: [false]
            };
		},
        created () {
            this.$http.get('/api/goods').then((response) => {
                this.goodList = response.data.data;
            });
        },
        mounted () {
        },
        methods: {
            // 根据返回type设置icon样式
            getIconType (type) {
                return 'type' + type;
            },
            // 给每一个food list item title设置id
            foodAnchor (index) {
                return 'foodTitle' + index;
            },
            // 改变menu list背景颜色以及字体粗细，首先初始化所有list item，然后改变选中的item
            changeMenuBg (j) {
                for (let i = 0; i < this.goodList.length; i++) {
                    this.$set(this.menuClick, i, false);
                };
                this.$set(this.menuClick, j, true);
            },
            // 控制menu list wrap的滑动，当food list wrap改变时候，控制scrollTop
            // i是food list title的index，
            // goodList.length 是list的数量
            // overflowH是超出的高度
            // fullIndex是未溢出的最后一个index
            contrlMenuWrap (i) {
                if (i === this.fullIndex) {
                    this.$el.querySelector('.menu_wrap ul').scrollTop = this.overflowH;
                } else if (i === this.goodList.length - this.fullIndex) {
                    this.$el.querySelector('.menu_wrap ul').scrollTop = 0;
                };
            },
            // menu list item点击事件后，控制food list wrap的scrollTop，模拟锚点的效果
            anchor (index) {
                this.scrollEvent = false;
                if (this.clicked) {
                    for (let i = 0; i < this.goodList.length; i++) {
                        this.menuNameP[i] = this.$refs.menuNameTop[i].offsetTop;
                        this.foodTitleP[i] = this.$refs.foodTitleTop[i].offsetTop;
                        this.foodTitleFixed[i] = false;
                    };
                    this.clicked = false;
                }
                this.changeMenuBg(index);
                this.$el.querySelector('.food_wrap_ul').scrollTop = this.foodTitleP[index];
                let _this = this;
                setTimeout(function () {
                    _this.scrollEvent = true;
                }, 1);
            },
            // food list wrap 滑动事件，并监控其scrollTop,首次通过滑动时间出发一个一次性事件，得出goodList.length，overflowH和fullIndex
            // 然后通过循环判断，操作menu list wrap的scrollTop，使之滑动
            scroll_event () {
                var scrollTop = this.$el.querySelector('.food_wrap_ul').scrollTop;
                if (this.scrollOnOff) {
                    this.scrollOnOff = false;
                    for (let i = 0; i < this.goodList.length; i++) {
                        this.menuNameP[i] = this.$refs.menuNameTop[i].offsetTop;
                        this.foodTitleP[i] = this.$refs.foodTitleTop[i].offsetTop;
                        this.foodTitleFixed[i] = false;
                    };
                    let liH = parseInt(window.getComputedStyle(this.$el.querySelector('.menu_wrap ul li')).height);
                    let viewH = parseInt(window.getComputedStyle(this.$el.querySelector('.menu_wrap ul')).height);
                    this.overflowH = liH * (this.goodList.length + 1) - viewH;
                    this.fullIndex = Math.floor(viewH / liH);
                };
                if (this.scrollEvent) {
                    for (let i = 0; i < this.goodList.length; i++) {
                        this.foodTitleFixed[i] = false;
                        if (scrollTop > this.foodTitleP[i] && scrollTop < this.foodTitleP[i + 1]) {
                            this.changeMenuBg(i);
                            this.contrlMenuWrap(i);
                            this.$set(this.foodTitleFixed, i, true);
                        } else if (scrollTop > this.foodTitleP[i] && i === this.goodList.length - 1) {
                            this.changeMenuBg(i);
                            this.contrlMenuWrap(i);
                            this.$set(this.foodTitleFixed, i, true);
                        } else if (scrollTop === 0) {
                            this.$set(this.foodTitleFixed, 0, false);
                        };
                    };
                };
            },
            clickPlus (p, food) {
                this.totalNum ++;
                if (this.pitchFoods[encodeURI(food.name)]) {
                    this.pitchFoods[encodeURI(food.name)][0] ++;
                } else {
                    this.pitchFoods[encodeURI(food.name)] = [1, food];
                };
                this.totalP += p;
            },
            clickReduce (p, food) {
                if (this.totalL === 1) {
                    this.shopcartDetail = false;
                };
                this.totalNum --;
                if (this.pitchFoods[encodeURI(food.name)] && this.pitchFoods[encodeURI(food.name)][0] === 1) {
                    delete this.pitchFoods[encodeURI(food.name)];
                } else {
                    this.pitchFoods[encodeURI(food.name)][0] --;
                };
                this.totalP -= p;
            },
            clickPlusShop (n, p) {
                this.reRender = false;
                this.totalNum ++;
                this.totalP += p;
                this.pitchFoods[encodeURI(n)][0] ++;
                this.reRender = true;
            },
            clickReduceShop (n, p) {
                this.reRender = false;
                this.totalNum --;
                this.totalP -= p;
                this.pitchFoods[encodeURI(n)][0] --;
                this.reRender = true;
            },
            fakeNumC (n) {
                if (this.pitchFoods[encodeURI(n)]) {
                    return this.pitchFoods[encodeURI(n)][0];
                } else {
                    return 0;
                }
            },
            clearAllItems () {
                this.shopcartDetail = false;
                this.totalNum = 0;
                this.totalP = 0;
                this.pitchFoods = {};
            },
            showFood (index, event) {
                if (event.target.className.indexOf('item_a') === -1) {
                   this.$set(this.showFoodWrap, index, true);
               }
            },
            backTo () {
                for (let i = 0; i < this.showFoodWrap.length; i++) {
                    this.$set(this.showFoodWrap, i, false);
                };
            }

        },
        components: {
            vShopBtn: shopBtn,
            vshopcart: shopcart,
            vfood: food
        }
	};
</script>

<style>
	.goods{
		display: flex;
		width:100%;
		height:auto;
		position: absolute;
		top:175px;
		bottom:0px;
		overflow:hidden;
        padding-bottom: 54px;
	}
	.menu_wrap{
        width:25%;
        height:100%;
        background-color: #f3f5f7;
	}
    .menu_wrap ul::-webkit-scrollbar{
        display: none;
    }
	.menu_wrap ul{
		width:100%;
		margin:0 auto;
		height:100%;
		overflow: auto;
	}
    .menu_wrap ul li:last-child{
        margin: 0 0 50px 0;
    }
	.good_name{
		width:90%;
        padding: 0 5%;
		height:50px;
		display: flex;
		justify-content:center;
		align-content:center;
		align-items:center;
		border-bottom:1px solid grey;
        position: relative;
	}
    .link_to{
        width: 100%;
        height: 100%;
        position: absolute;
        left: 0;
        top: 0;
    }

	.good_name .text{
		font-size: 14px;
		vertical-align: top;
		line-height:22px;
	}
    .type0{
    	vertical-align: top;
    	display: inline-block;
    	width: 22px;
    	height: 22px;
    	margin-right: 2px;
    	background:url(./images/decrease_3@2x.png) no-repeat center center;
    	background-size: 22px 22px;
    }
    .type1{
    	vertical-align: top;
    	display: inline-block;
    	width: 22px;
    	height: 22px;
    	margin-right: 2px;
    	background:url(./images/discount_3@2x.png) no-repeat center center;
    	background-size: 22px 22px;
    }
    .type2{
    	vertical-align: top;
    	display: inline-block;
    	width: 22px;
    	height: 22px;
    	margin-right: 2px;
    	background:url(./images/special_3@2x.png) no-repeat center center;
    	background-size: 22px 22px;
    }
    .type3{
    	vertical-align: top;
    	display: inline-block;
    	width: 22px;
    	height: 22px;
    	margin-right: 2px;
    	background:url(./images/invoice_3@2x.png) no-repeat center center;
    	background-size: 22px 22px;
    }
    .type4{
    	vertical-align: top;
    	display: inline-block;
    	width: 22px;
    	height: 22px;
    	margin-right: 2px;
    	background:url(./images/guarantee_3@2x.png) no-repeat center center;
    	background-size: 22px 22px;
    }


    .food_wrap{
    	width:75%;
    	height:100%;
    }
    .food_wrap ul::-webkit-scrollbar{
        display: none;
    }
    .food_wrap ul{
        width:100%;
        height:100%;
        overflow: auto;
        position: relative;
    }
    .food_list{
        width:100%;
    	height:auto;

    }
    .food_list_item{
        width:100%;
    	height:auto;
    }

    .food_title{
    	width:98%;
        margin-left: 2%;
    	height:40px;
    	line-height: 40px;
        border-bottom: 1px solid grey;
    }
    .food_title_fixed{
        width:73.5%;
        background-color:#fff;
        position: fixed;
        right:0;
        top:175px;
    }
    .food_detail{
    	width:100%;
    	height:120px;
    }
    .food_detail_left{
    	display: inline-block;
    	vertical-align: top;
    	width: 90px;
    	height:90px;
    	margin: 15px 0 0 10px;
    }
    .food_detail_left img{
    	display: inline-block;
    	vertical-align: top;
    	width: 90px;
    	height:90px;
    }
    .food_detail_right{
    	display: inline-block;
    	vertical-align: top;
        width: 160px;
        height:90px;
    	margin: 15px 0 0 6px;
    }


    .food_name{
    	font-size: 18px;
        line-height: 24px;
    }
    .des_rat_n{
    	font-size: 14px;
        color: grey;
        line-height: 24px;
        width: 100%;
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
    }
    .price_num_wrap{
        font-size: 0;
        margin-top: 4px;
    }
    .price{
    	font-size: 20px;
        line-height: 24px;
        color: red;
    }
    .oldPrice{
        text-decoration: line-through;
    }
    .whiteBg{
        background-color: #fff;
    }
    .whiteBg span{
        font-weight: bold;
    }
</style>
