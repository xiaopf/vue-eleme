<template>
	<div class="ratingSelect">
       <h2 class="ratingSelectTitle">商品评价</h2>
       <ul class="ratingSelectCard">
           <li v-on:click="changeShow(0)" class="card_li_01"><span> {{ foodChoiceType[0] }} </span> <span>{{ ratings.length }}</span> </li>
           <li v-on:click="changeShow(1)" class="card_li_02"><span> {{ foodChoiceType[1] }} </span> <span>{{ upNums() }}</span> </li>
           <li v-on:click="changeShow(2)" class="card_li_03"><span> {{ foodChoiceType[2] }} </span> <span>{{ratings.length - upNums()}}</span> </li>
       </ul>
       <div>
          <hr>
          <div class="ratingSelectChoice" v-on:click="changeRight">
              <span class="noright" v-bind:class="{ right : right }"></span>
              <span v-bind:class="{ font_blue : right }">只看内容和评价</span>
          </div>
          <hr>
          <ul class="ratingSelectItems" v-if="reRender">
              <li v-for="rating in ratings" v-if="showOrNot(rating.rateType)">

                    <div v-if="!rating.score">
                        <p v-if="!right" class="rating_p_01">
                           <span class="rating_01_span_01">{{rateTime(rating.rateTime)}}</span>
                           <span class="rating_01_span_03"><img v-bind:src="rating.avatar" alt=""></span>
                           <span class="rating_01_span_02">{{rating.username}}</span>
                        </p>
                        <p class="rating_p_02">
                           <span v-bind:class="rateType(rating.rateType)" class="rating_02_span_01"></span>
                           <span class="rating_02_span_02">{{rating.text}}</span>
                        </p> 
                    </div>
                    <div v-else>
                        <div class="ratings_img_name_star_wrap">
                            <div class="ratings_img"><img v-bind:src="rating.avatar" alt=""></div>
                            <div class="ratings_name_star">
                                <p class="ratings_name_star_p01">                   
                                    <span>{{rating.username}}</span>
                                    <span v-if="!right" class="ratings_time">{{rateTime(rating.rateTime)}}</span>
                                </p>
                                <p class="ratings_name_star_p02">
                                    <span><vstar v-bind:score="rating.score" v-bind:size="-1"></vstar></span>
                                    <span v-if="rating.deliveryTime && !right">{{ rating.deliveryTime }}分钟送达</span>
                                </p>
                            </div>
                        </div>
                        <p v-if="rating.text" class="ratings_text">{{rating.text}}</p>
                        <div v-if="!right" class="ratings_type_recommend">
                            <p class="ratings_type" v-bind:class="rateType(rating.rateType)"></p>
                            <p class="ratings_recommend">
                                <span v-for="recommend in rating.recommend">{{recommend}}</span>
                            </p>
                        </div>
                    </div>
              </li>
          </ul> 
       </div>
	</div>
</template>

<script type='text/ecmascript-6'>
    import star from '../star/star';
	export default {
      props: {
        ratings: Array,
        foodChoiceType: Array
      },
      data () {
        return {
            right: false,
            ratingCard: [true, false, false],
            reRender: true
        };
      },
      computed: {
      },
      methods: {
        rateTime (time) {
            var d = new Date();
            d.setTime(time);
            return d.toLocaleString();
        },
        rateType (type) {
            if (type === 0) {
                return 'down';
            } else {
                return 'up';
            }
        },
        changeRight () {
            if (this.right) {
                this.right = false;
            } else {
                this.right = true;
            };
        },
        changeShow (num) {
            this.reRender = false;
            for (let i = 0; i < this.ratingCard.length; i++) {
                this.ratingCard[i] = false;
            };
            this.ratingCard[num] = true;
            this.reRender = true;
        },
        showOrNot (type) {
            if (this.ratingCard[0]) {
                return true;
            } else if (this.ratingCard[2] && type === 0) {
                return true;
            } else if (this.ratingCard[1] && type === 1) {
                return true;
            };
            return false;
        },
        upNums () {
            let num = 0;
            for (let i = 0; i < this.ratings.length; i++) {
               if (this.ratings[i].rateType === 1) {
                  num++;
               }
            };
            return num;
        }
      },
        components: {
            vstar: star
        }
	};
</script>
<style>
	.ratingSelect{
        height:auto;
        width:100%;
    }
    .ratingSelectTitle{
        font-size:20px;
        line-height: 34px;
        height:34px;
        padding:18px 18px 0 18px;
    }
    .ratingSelect .ratingSelectCard{
        padding:12px 18px;
        font-size: 0;
    }
    .ratingSelectCard li{
        padding:0 10px;
        height:36px;
        display:inline-block;
        font-size: 16px;
        margin-right: 8px;
        line-height:36px;
        text-align:center;
        border-radius:4px;
    }
    .card_li_01{
        background-color:#008fe1;
        color:#fff;
    }
    .card_li_02{
        background-color:#99d8fc;
    }
    .card_li_03{
        background-color:#babfc2;
    }
    .ratingSelectChoice{
       padding:12px 18px; 
       height:30px;
       line-height: 30px;
    }
    .rating_p_02 .up,.ratings_type_recommend .up{
        display: inline-block;
        width: 24px;
        height: 24px;
        background:url(./images/up.png) no-repeat center center;
        background-size: 18px 18px;
        font-size: 0
    }
    .rating_p_02 .down,.ratings_type_recommend .down{
        display: inline-block;
        font-size: 24px;
        vertical-align: top;
        width: 24px;
        height: 24px;
        background:url(./images/down.png) no-repeat center center;
        background-size: 18px 18px;
    }
    .ratingSelectChoice span{
        display: inline-block;
        vertical-align: top;
        font-size: 16px;
        height: 24px;
        line-height: 24px;
        vertical-align: top;
        color:grey;
    }
    .ratingSelectChoice .noright{
        font-size: 24px;
        vertical-align: top;
        width: 24px;
        background:url(./images/noright.png) no-repeat center center;
        background-size: 24px 24px;
    }
    .ratingSelectChoice .right{
        font-size: 24px;
        vertical-align: top;
        width: 24px;
        background:url(./images/right.png) no-repeat center center;
        background-size: 24px 24px;
        font-size: 0
    }

    .font_blue{
        color:#00c850!important;
    }
    .ratingSelectItems{
        width:auto;
        padding:0px 18px 26px;
        height:auto;
    }
    .ratingSelectItems>li{
        width:100%;
        padding: 12px 0 8px 0;
        border-bottom:1px solid grey;
    }
    .ratingSelectItems .rating_p_01{
        margin-bottom: 10px;
        font-size: 0;
    }
    .ratingSelectItems .rating_p_02{
        margin-bottom: 6px;
    }
    .ratingSelectItems .rating_p_01 .rating_01_span_01{
        font-size: 14px;
        vertical-align:top;
        height:24px;
        line-height:24px;
        display: inline-block;
    }
    .ratingSelectItems .rating_p_01 .rating_01_span_02{
        font-size: 14px;
        float:right;
        vertical-align:top;
        height:24px;
        line-height:24px;
        display: inline-block;
    }
    .ratingSelectItems .rating_p_01 .rating_01_span_03{
        font-size: 14px;
        float:right;
        vertical-align:top;
        display: inline-block;
        width:24px;
        height:24px;
        border-radius:50%;
        margin: 0 6px;
    }
    .ratingSelectItems .rating_p_01 .rating_01_span_03 img{
        width:24px;
        height:24px;
        border-radius:50%;
    }
    .ratingSelectItems .rating_p_02 .rating_02_span_01{

    }
    .ratingSelectItems .rating_p_02 .rating_02_span_02{
        font-size: 18px;
        color:#000;
        line-height: 24px;
    }
    .ratings_img{
        vertical-align:top;
        display: inline-block;
        width:36px;
        height:36px;
        border-radius:50%;
        margin: 0 4px 0 0;
        padding-bottom: 6px;
    }
    .ratings_img_name_star_wrap{
        position: relative;
    }
    .ratings_img>img{
        width:36px;
        height:36px;
        border-radius:50%;
    }
    .ratings_name_star{
        vertical-align:top;
        display: inline-block;
        height:36px;
        line-height:18px;
        padding-bottom: 4px;
    }
    .ratings_name_star>p>span{
        vertical-align:top;
        display: inline-block;
        font-size: 14px;
        line-height:18px;
    }
    .ratings_name_star_p01{
        display: block;
    }
    .ratings_name_star_p02{

    }
    .ratings_text{
        padding: 4px 0 4px 40px;
        font-size:16px;
        line-height: 22px;
    }
    .ratings_type_recommend{
        margin:4px 0 4px 40px;
    }
    .ratings_type{
        display: inline;
        vertical-align: top;
        margin-top: 5px;
    }
    .ratings_recommend{
        display: inline;
        vertical-align: top;

    }
    .ratings_recommend span{
        display: inline-block;
        padding:3px 6px;
        height:16px;
        font-size: 14px;
        color:grey;
        border:1px solid grey;
        margin:4px;
        border-radius:4px;
    }
    .ratings_time{
        position: absolute;
        right:0px;
        top:0px;
        height:18px;
        line-height: 18px;
        font-size:14px;
    }
</style>
