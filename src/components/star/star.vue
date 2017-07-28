<template>
	<div class="star_wrap">
	  <span v-if="size > 0" v-for="item in items" v-bind:class="item" class="stars"></span>
      <span v-if="size === 0" v-for="item in items" v-bind:class="item" class="stars_mini"></span>
      <span v-if="size < 0" v-for="item in items" v-bind:class="item" class="stars_ms"></span>
	</div>
</template>

<script type='text/ecmascript-6'>
    const STAR_LEN = 5;
    export default {
        props: {
            score: {
                type: Number
            },
            size: {
                type: Number
            }
        },
        computed: {
            items () {
                let result = [];
                let resultMini = [];
                let resultMs = [];
                let full = Math.floor(this.score);
                let half = Math.floor(this.score % 1 * 2);
                let none = STAR_LEN - full - half;
                for (let i = 0; i < full; i++) {
                    result.push('fullStar');
                    resultMini.push('fullStar_mini');
                    resultMs.push('fullStar_ms');
                };
                 for (let i = 0; i < half; i++) {
                    result.push('halfStar');
                    resultMini.push('halfStar_mini');
                    resultMs.push('halfStar_ms');
                };
                 for (let i = 0; i < none; i++) {
                    result.push('noneStar');
                    resultMini.push('noneStar_mini');
                     resultMs.push('noneStar_ms');
                };
                if (this.size > 0) {
                    return result;
                } else if (this.size === 0) {
                    return resultMini;
                } else {
                    return resultMs;
                }
            }
        }
    };
</script>

<style>
    .star_wrap{
        font-size: 0;
        display: inline-block;
        vertical-align: top;
    }
    .stars{
        width: 28px;
        height: 27px;
        display: inline-block;
        margin: 5px 5px;
    }
    .fullStar{
        background: url(images/star36_on@2x.png) no-repeat center center;
        background-size: 28px 27px;
    }
    .halfStar{
        background: url(images/star36_half@2x.png) no-repeat center center;
        background-size: 28px 27px;
    }
    .noneStar{
        background: url(images/star36_off@2x.png) no-repeat center center;
        background-size: 28px 27px;
    }
    .stars_mini{
        width: 20px;
        height: 20px;
        display: inline-block;
        margin: 2px 2px;
    }
    .fullStar_mini{
        background: url(images/star36_on@2x.png) no-repeat center center;
        background-size: 20px 20px;
    }
    .halfStar_mini{
        background: url(images/star36_half@2x.png) no-repeat center center;
        background-size: 20px 20px;
    }
    .noneStar_mini{
        background: url(images/star36_off@2x.png) no-repeat center center;
        background-size: 20px 20px;
    }

    .stars_ms{
        width: 12px;
        height: 12px;
        display: inline-block;
        margin: 2px 2px;
    }
    .fullStar_ms{
        background: url(images/star36_on@2x.png) no-repeat center center;
        background-size: 12px 12px;
    }
    .halfStar_ms{
        background: url(images/star36_half@2x.png) no-repeat center center;
        background-size: 12px 12px;
    }
    .noneStar_ms{
        background: url(images/star36_off@2x.png) no-repeat center center;
        background-size: 12px 12px;
    }
</style> 
