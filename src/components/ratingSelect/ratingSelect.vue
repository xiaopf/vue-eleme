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
                  <p v-if="!right" class="rating_p_01">
                      <span class="rating_01_span_01">{{rateTime(rating.rateTime)}}</span>
                      <span class="rating_01_span_03"><img v-bind:src="rating.avatar" alt=""></span>
                      <span class="rating_01_span_02">{{rating.username}}</span>
                  </p>
                  <p class="rating_p_02">
                      <span v-bind:class="rateType(rating.rateType)" class="rating_02_span_01"></span>
                      <span class="rating_02_span_02">{{rating.text}}</span>
                  </p>
              </li>
          </ul> 
       </div>

	</div>
</template>

<script type='text/ecmascript-6'>
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
    .rating_p_02 .up{
        display: inline-block;
        width: 24px;
        height: 24px;
        background:url(./images/up.png) no-repeat center center;
        background-size: 18px 18px;
        font-size: 0
    }
    .rating_p_02 .down{
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
        padding: 16px 0;
        border-bottom:1px solid grey;
    }


    .ratingSelectItems .rating_p_01{
        margin-bottom: 10px;
        font-size: 0;
    }
    .ratingSelectItems .rating_p_02{

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
</style>
