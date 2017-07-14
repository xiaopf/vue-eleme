<template>
	<div class="header">
	    <img class="bgp" :src="seller.avatar">
		<div class="wrap_top">
			<img class="avatar" :src="seller.avatar">
			<div class="text_wrap">
				<div class="sname"><span class="brand"></span><span>{{ seller.name }}</span></div>
				<p class="description">{{ seller.description }} / {{ seller.deliveryTime }}分钟送达</p>
				<div v-if="seller.supports">
					<div class="supports">
						<span class="sale decrease"></span>
						<span>{{ seller.supports[0].description }}</span>
					</div>
					<div class="more_supports" v-on:click="showDetail">{{seller.supports.length}}个 ></div>
				</div>
			</div>
		</div>
		<div class="bulletin" v-on:click="showDetail">
			<span></span>
			<span class="bulletin_content">{{ seller.bulletin }}</span>
			<span>></span>
		</div>
		<div class="detail" v-show="detailShow">
			<div class="detail_wrap">
				<div class="detail_content">
				    <div class="detail_name">{{ seller.name }}</div>
					<div class="vstar_wrap">
						<vstar v-bind:score=seller.score v-bind:size="8"></vstar>
					</div>
					<div class="title">
						<div class="line"></div>
						<div class="text">优惠信息</div>
						<div class="line"></div>
					</div>
					<ul v-if=seller.supports class="supports_all">
						<li v-for="typeItem in seller.supports" class="supports_item">
							<span v-bind:class="icon_class[typeItem.type]"></span>
							<span> {{ typeItem.description }} </span>
						</li>
					</ul>
					<div class="title">
						<div class="line"></div>
						<div class="text">商家公告</div>
						<div class="line"></div>
					</div>
					<div class="bulletin_tt">{{ seller.bulletin }}</div>
				</div>
			</div>
			<div class="detail_close">
				<span @click="closeDetail" class="fa fa-close"></span>
			</div>
		</div>
	</div>
</template>

<script type='text/ecmascript-6'>
    import star from '../star/star.vue';
    export default {
        props: {
            seller: {
                type: Object
            }
        },
        data () {
            return {
                detailShow: false,
                icon_class: ['type0', 'type1', 'type2', 'type3', 'type4']
            };
        },
        methods: {
            showDetail () {
                this.detailShow = true;
            },
            closeDetail () {
                this.detailShow = false;
            }
        },
        components: {
            vstar: star
        }
    };
</script>

<style>
	.header{
		width:100%;
		font-size: 0;
		background-color: rgba(7,17,27,0.5);
		position: relative;
		overflow: hidden;
	}
	/* 背景底图片 */
	.bgp{
        position: absolute;
        left: 0;
        top: 0;
        z-index: -1;
        width: 100%;
        height: 134px;
        filter: blur(10px);
	}
	/* header的上半部分 */
	.wrap_top{
		padding: 24px 0 0 24px;
	}
	/* 商店图片 */
	.avatar{
        display: inline-block;
		width: 64px;
		height: 64px;
		border-radius: 2px;
		vertical-align: top;
		margin-bottom: 18px;
		
	}
	/* 右侧的文字部分 */
	.text_wrap{
        display: inline-block; 
        width:72%;
        margin-left: 16px;   
        margin-top: 2px;
	}

	/* 商店的名称 */
	.sname{
		display: inline-block;
		font-size: 16px;
		color: #fff;
		line-height: 16px;
		height:18px;
		font-weight: bold;
		margin-bottom: 8px;
	}
	/* 商店名称的icon图标 */
	.brand{
		display: inline-block;
		width: 30px;
		height: 18px;
		line-height: 18px;
		background: url(./images/brand@2x.png) no-repeat center center; 
		background-size: 30px 18px;
		margin:0 6px 0 0;
		vertical-align: top;
	}
	.sname span:last-child{
		display: inline-block;
		line-height: 18px;
		height:18px;
	}

	.description{
		font-size: 14px;
		line-height: 12px;
		color: #fff;
		line-height: 12px;
		margin-bottom: 10px;
	}
	/* 活动部分 */
	.supports{
		display: inline-block;
		font-size: 14px;
		color: #fff;
	}
	.supports .sale{
		display: inline-block;
		width: 12px;
		height: 14px;
		line-height: 14px;
		vertical-align: top;
		margin-right: 2px;
	}
	.supports span:last-child{
		display: inline-block;
		height: 14px;
		line-height: 14px;
	}
	.more_supports{
		display: inline-block;
		font-size: 14px;
		color: #fff;
		width: 48px;
		height: 24px;
		background-color: rgba(0,0,0,0.2);
		line-height: 24px;
		text-align: center;
		border-radius: 8px;
		margin-right:12px;
		margin-top: -5px;
		float:right; 
	}

	/*活动的icon图标*/
	.decrease{
		background:url(./images/decrease_1@2x.png) no-repeat center center;
		background-size: 12px 12px;
	}
	.discount{
		background:url(./images/discount_1@2x.png) no-repeat center center;
		background-size: 12px 12px;
	}
	.guarantee{
		background:url(./images/guarantee_1@2x.png) no-repeat center center;
		background-size: 12px 12px;
	}
	.invoice{
		background:url(./images/invoice_1@2x.png) no-repeat center center;
		background-size: 12px 12px;
	}
	.special{
		background:url(./images/special_1@2x.png) no-repeat center center;
		background-size: 12px 12px;
	}
    /* 公告区域*/
	.bulletin{
		height: 28px;
		background-color: rgba(7,17,27,0.2);
		font-size: 10px;
		color:#fff;
	}
	.bulletin span:first-child{
		display: inline-block;
		width: 30px;
		height: 28px;
		background: url(./images/bulletin@2x.png) no-repeat center center;
		background-size: 30px 18px;
		margin:0 4px 0 12px;
	}
	.bulletin span:last-child{
		display: inline-block;
		height: 28px;
		line-height: 28px;
		position: absolute;
		right:0;
		margin:0 12px 0 4px;
	}
	.bulletin .bulletin_content{
		display: inline-block;
		height: 28px;
		line-height: 28px;
		overflow:hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
		width: 80%;
	}
	.detail{
		width: 100%;
		height: 100%;
		position: fixed;
		top: 0;
		left: 0;
		z-index: 99;
		overflow: auto;
		background: rgba(7,17,27,0.8);
	}
	.detail_wrap{
		width: 100%;
		min-height: 100%;
	}
	.detail_content{
		width: 100%;
		padding: 64px 0;
	}
	.detail_name{
		font-size: 20px;
		height: 20px;
		text-align: center;
		color:#fff;
		font-weight: bold;

	}
	.detail_close{
		width: 100%;
		font-size: 32px;
		height: 32px;
		width: 32px;
		margin:-64px auto 0;
	}

	.vstar_wrap{
		text-align: center;
		margin: 12px 0;
	}

	.title{
        width: 80%;
        height: auto;
        display: flex;
        margin: 0 auto;
	}
	.title .line{
       height:0;
       width: 90%;
       border-bottom: 1px solid grey;
       position: relative;
       top:10px;
       flex:1;

	}
	.title .text{
	   height:24px;
	   width: 100px;
       font-size: 18px;
       font-weight: bold;
       color:#fff;
       text-align: center;
	}
	.supports_all{
		display: block;
		width: 80%;
		height: auto;
		margin: 20px auto;
		
	}
	.supports_item{
		display: block;
		font-size: 0;
		width: 100%;
		height: 28px;
		margin: 8px 0;
	}
	.supports_item span:first-child{
		vertical-align: top;
		width: 28px;
		height: 28px;
        display: inline-block;
        line-height: 28px;
        margin-right: 6px;
	}
	.supports_item span:last-child{
		vertical-align: top;
		width: auto;
		height: 28px;
		font-size: 14px;
        display: inline-block;
        line-height: 28px;
        color: #fff;
	}
	.type0{
		background:url(./images/decrease_2@2x.png) no-repeat center center;
		background-size: 22px 22px;
	}
	.type1{
		background:url(./images/discount_2@2x.png) no-repeat center center;
		background-size: 22px 22px;
	}
	.type2{
		background:url(./images/special_2@2x.png) no-repeat center center;
		background-size: 22px 22px;
	}
	.type3{
		background:url(./images/invoice_2@2x.png) no-repeat center center;
		background-size: 22px 22px;
	}
	.type4{
		background:url(./images/guarantee_2@2x.png) no-repeat center center;
		background-size: 22px 22px;
	}

	.bulletin_tt{
		margin: 10px auto;
		width: 80%;
		height:auto;
		font-size: 16px;
		color:#fff;
		line-height: 26px;
		text-indent: 2em;
		background: transparent;
	}


</style> 
