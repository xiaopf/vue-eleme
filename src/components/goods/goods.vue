<template>
	<div class="goods">
		<div class="menu_wrap">
			<ul>
				<li v-for="good in goodList" class="good_name">
					<span class="text">
						<span v-bind:class="icon_class_good[good.type]"></span>{{good.name}}	
					</span>
				</li>
			</ul>
		</div>
		<div class="food_wrap">
			<ul>
				<li v-for="good in goodList" class="food_list">
                     <div v-for="(food,index) in good.foods" class="food_list_item">
                        <h3 v-if="index===0" class="food_title">{{good.name}}</h3>
                        <div class="food_detail">
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
                                <p>
	                                <span class="price">
	                                	<span>￥</span><span>{{food.price}}</span>
	                                </span>
	                                <span class="des_rat_n oldPrice">￥{{food.oldPrice}}</span>
                                </p>
                               
                            </div>
                        </div>
                     	
                     </div>
				</li>
			</ul>
		</div>
	</div>
</template>

<script type='text/ecmascript-6'>
	export default {
		data () {
            return {
                goodList: [],
                foodList: [],
                icon_class_good: ['type0', 'type1', 'type2', 'type3', 'type4']
            };
		},
        created () {
            this.$http.get('/api/goods').then((response) => {
                this.goodList = response.data.data;
            });
        }
	};
</script>

<style>
	.goods{
		display: flex;
		width:100%;
		height:auto;
		position: absolute;
		top:174px;
		bottom:60px;
		overflow:hidden;
	}
	.menu_wrap{
        width:25%;
        height:100%;
        background-color: #f3f5f7;
	}
	.menu_wrap ul{
		width:90%;
		margin:0 auto;
		height:100%;
		overflow: auto;
		
	}
	.good_name{
		width:100%;
		height:50px;
		display: flex;
		justify-content:center;
		align-content:center;
		align-items:center;
		border-bottom:1px solid grey;
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
    .food_list{
    	width:96%;
    	margin:0 auto;
    	height:auto;

    }
    .food_list_item{
    	width:100%;
    	height:160px;
    }

    .food_title{
    	width:100%;
    	height:40px;
    	line-height: 40px;
    	background-color: #f3f5f7;
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
    	margin: 15px 0 0 10px;
    }
    .food_detail_right{
    	display: inline-block;
    	vertical-align: top;
    	margin: 15px 0 0 10px;
    }

    .food_name{
    	font-size: 20px;
    }
    .des_rat_n{
    	font-size: 12px;
    }
    .price{
    	font-size: 22px;
    }
    .oldPrice{
    	under 
    }
</style> 
