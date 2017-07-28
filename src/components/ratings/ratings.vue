<template>
	<div class="ratings">
		<div class="ratings_div">
			<div class="ratings_wrap">
				<div class="ratings_left">
					<p class="ratings_left_p01">{{ seller.score }}</p>
					<p class="ratings_left_p02">综合评分</p>
					<p class="ratings_left_p03">高于周边商家{{ seller.rankRate }}%</p>
				</div>
				<div class="midlle_line"></div>
				<div class="ratings_right">
					<p class="ratings_right_p01">
						<span>食品评价</span>
						<span><vstar v-bind:score="seller.foodScore" v-bind:size="0"></vstar></span>
					</p>
					<p class="ratings_right_p02">
						<span>服务态度</span>
						<span><vstar v-bind:score="seller.serviceScore" v-bind:size="0"></vstar></span>
					</p>
					<p class="ratings_right_p03">
						<span>送达时间</span>
						<span>{{ seller.deliveryTime }}分钟送达</span>
					</p>
				</div>	
			</div>
			<div class="line_grey"></div>
			<vratingSelect v-bind:ratings="ratings" v-bind:foodChoiceType="foodChoiceType"></vratingSelect>
		</div>
	</div>
</template>

<script type='text/ecmascript-6'>
	import ratingSelect from '../ratingSelect/ratingSelect';
	import star from '../star/star';
	export default {
        data () {
            return {
                ratings: [],
                seller: {},
                foodChoiceType: ['全部', '满意', '不满意']
            };
        },
        created () {
            this.$http.get('/api/ratings').then((response) => {
                this.ratings = response.data.data;
            });
            this.$http.get('/api/seller').then((response) => {
                this.seller = response.data.data;
            });
        },
        components: {
            vratingSelect: ratingSelect,
            vstar: star
        }
	};
</script>

<style>

	.ratings{
		display: flex;
		width:100%;
		height:auto;
		position: absolute;
		top:175px;
		bottom:0px;
		overflow:hidden;
        padding-bottom: 0;
	}
	.ratings_div::-webkit-scrollbar{
	    display: none;
	}
	.ratings_div{
		width: 100%;
		overflow:auto;
	}
	.ratings_wrap{
		font-size:0;
		padding:12px 6px;
		display: flex;
		justify-content: space-around;
	}
	.ratings_left{
		width: 150px;
		display:inline-block;
		vertical-align:top;
	}
	.ratings_left p{
        text-align:center;
	}

	.midlle_line{
		height: 90px;
		border-right: 1px solid #c3c3c3;
		margin:0 10px;
	}
	.ratings_left_p01{
        font-size: 24px;
        line-height:40px;
        color:#ff9900;
	}
	.ratings_left_p02{
        font-size: 16px;
        line-height:30px;
        color:#000;
	}
	.ratings_left_p03{
        font-size: 12px;
        line-height:20px;
        color:grey;
	}

	.ratings_right{
		width: 210px;
		display:inline-block;
		vertical-align:top;
		text-align: center;
	}
	.ratings_right p{
		width: 210px;
		font-size:0;
		line-height: 33px;
		text-align: left;
	}
	.ratings_right p>span{
		display:inline-block;
		font-size: 16px;
		margin:0 4px;
		height:24px;
		line-height: 24px;
		vertical-align: top;
	}


	.ratings_right_p01{

	}
	.ratings_right_p02{

	}
	.ratings_right_p03 span:last-child{
		color:grey;
	}
</style> 
