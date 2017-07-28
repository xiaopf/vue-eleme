<template>
	<div class="seller">
		<div class="seller_div">
            <div class="seller_item1_wrap">
                <div class="collect_seller" v-on:click="heartColor = !heartColor">
                	<div class="heart heart_grey" v-bind:class="{heart_red : heartColor}"></div>
                	<p v-if="!heartColor">未收藏</p>
                	<p v-else style="color:#000;">收藏</p>
                </div>
            	<p class="seller_item1_wrap_name">{{ seller.name }}</p>
            	<p class="seller_item1_wrap_rating">
            		<span><vstar  v-bind:score="seller.foodScore" v-bind:size="0"></vstar></span>
            		<span>({{ seller.ratingCount}})</span>
            		<span>月售{{ seller.sellCount}}单</span>
            	</p>
            	<ul class="seller_ul_wrap">
            		<li>
            			<p class="seller_ul_li_p01">起送价</p>
            			<p>
            				<span class="seller_ul_li_p_span01">{{ seller.deliveryPrice }}</span><span class="seller_ul_li_p_span02">元</span>
            			</p>
            		</li>
            		<li class="seller_ul_li02">
            			<p class="seller_ul_li_p01">商家配送</p>
            			<p>
            				<span class="seller_ul_li_p_span01">{{ seller.minPrice }}</span><span class="seller_ul_li_p_span02">元</span>
            			</p>
            		</li>
            		<li>
            			<p class="seller_ul_li_p01">平均配送时间</p>
            			<p>
            				<span class="seller_ul_li_p_span01">{{ seller.deliveryTime }}</span><span class="seller_ul_li_p_span02">分钟</span>
            			</p>
            		</li>
            	</ul>
            </div>
			<div class="line_grey"></div>
				<div class="seller_item2_wrap">
                    <h2 class="seller_item2_title">公告与活动</h2>
                    <p class="seller_item2_text">{{ seller.bulletin }}</p>
                    	<ul v-if=seller.supports class="supports_all ">
                    		<li v-for="typeItem in seller.supports" class="supports_item">
                    			<span v-bind:class="icon_class[typeItem.type]"></span>
                    			<span> {{ typeItem.description }} </span>
                    		</li>
                    	</ul>
				</div>
			<div class="line_grey"></div>
				<div class="seller_item3_wrap">
                    <h2 class="seller_item3_title">商家实景图</h2>
                    <div class="seller_item3_ul_box">
	                    <ul class="seller_item3_ul">
	                    	<li class="seller_item3_pic" v-for="pic in seller.pics">
	                    		<img v-bind:src="pic" alt="">
	                    	</li>
	                    </ul>
                    </div>
				</div>
			<div class="line_grey"></div>
				<div class="seller_item4_wrap">
                    <h2 class="seller_item4_title">商家信息</h2>
                    <ul>
                    	<li class="seller_item4_text" v-for="info in seller.infos">{{info}}</li>
                    </ul>
				</div>
			<div class="line_grey"></div>
		</div>
	</div>
</template>

<script type='text/ecmascript-6'>
	import star from '../star/star';
	export default {
        data () {
            return {
                seller: {},
                icon_class: ['type0', 'type1', 'type2', 'type3', 'type4'],
                heartColor: false
            };
        },
		created () {
			this.$http.get('/api/seller').then((response) => {
				this.seller = response.data.data;
			});
		},
        components: {
            vstar: star
        }
	};
</script>

<style>
	.seller{
		display: flex;
		width:100%;
		height:auto;
		position: absolute;
		top:175px;
		bottom:0px;
		overflow:hidden;
	    padding-bottom: 0;
	}
	.seller_div::-webkit-scrollbar{
	    display: none;
	}
	.seller_div{
		width: 100%;
		overflow:auto;
	}
	.seller_item1_wrap{
        padding: 18px;
        position: relative;
	}
	.seller_item1_wrap_name{
		font-size: 20px;
		font-weight:bold;
		height:28px;
		line-height: 28px;
	}
	.seller_item1_wrap_rating{
		margin: 8px 0 0 0;
		padding-bottom: 12px;
		height:28px;
		line-height: 28px;
	}
	.seller_item1_wrap_rating>span{
		display: inline-block;
		vertical-align: top;
		height:28px;
		line-height: 28px;
		margin-right: 8px;
	}
	.seller_ul_wrap{
        display: flex;
        justify-content:center;
	}
	.seller_ul_wrap>li{
		flex:1;
		text-align: center;
		border-top: 1px solid #efefef;
		border-bottom: 1px solid #efefef;
		padding: 18px 0;
	}
	.seller_ul_li02{
		border-left: 1px solid #efefef;
		border-right: 1px solid #efefef;
	}
	.seller_ul_li_p01{
		color:grey;
		font-size: 14px;
		line-height: 20px;
	}
	.seller_ul_li_p_span01{
		color:#000;
		font-size: 24px;
		line-height: 30px;
	}
	.seller_ul_li_p_span02{
		color:#000;
		font-size: 12px;
		line-height: 30px;
	}

	.seller_item2_wrap,.seller_item3_wrap,.seller_item4_wrap{
		padding:12px 18px;
	}
	.seller_item2_title,.seller_item3_title,.seller_item4_title{
		font-size:20px;
		line-height: 40px;
		height:40px;
		font-weight: bold;
	}
	.seller_item2_text{
		font-size:16px;
		line-height: 28px;
		color:red;
		padding: 2px 12px;
		letter-spacing: 1px;
	}
	.seller_item2_wrap .supports_all{
		margin:16px 0;
		width:auto;
	}
	.seller_item2_wrap .supports_all .supports_item{
		margin:0;
		width: auto;
		padding:10px 0 10px 12px;
		border-top:1px solid #e3e2e1;
	}
	.seller_item2_wrap .supports_all>li:last-child{
		border-bottom:1px solid #e3e2e1;
	}
	.seller_item2_wrap .supports_all .supports_item span{
		color:#000;
		font-size:16px;
	}
	.seller_item3_ul_box::-webkit-scrollbar{
	    display: none;
	}
	.seller_item3_ul_box{
		width: 100%;
		height:190px;
		overflow-x:scroll;
	}
	.seller_item3_ul{
		width: auto;
		white-space: nowrap;
	}
	.seller_item3_pic{
		width: 240px;
		height:180px;
		margin:0 6px;
		display:inline-block;
	}
	.seller_item3_pic img{
		width: 240px;
		height:180px;
	}
	.seller_item4_text{
		width: auto;
		line-height: 28px;
		padding:10px 0 10px 12px;
		border-top:1px solid #e3e2e1;
		color:#000;
		font-size:16px;
	}
	.seller_item4_wrap>ul>li:last-child{
		border-bottom:1px solid #e3e2e1;
	}

.collect_seller{
    position: absolute;
    right:24px;
    top:26px;
}
.collect_seller p{
	width:60px;
	text-align: center;
	height:20px;
	line-height:32px;
	font-size: 16px;
	color:#a0a4a2;
}
.heart{
	width:20px;
	height:20px;
	padding-left: 40px;
}
.heart_grey{
    background:url(./images/heart_grey.png) no-repeat center center;
    background-size: 20px 20px;
}
.heart_red{
    background:url(./images/heart_red.png) no-repeat center center;
    background-size: 20px 20px;
}

</style> 
