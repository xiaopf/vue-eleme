<template>
	<div class="star_wrap">
	  <span v-for="item in items" v-bind:class="item" class="stars">{{ item }}</span>
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
                let full = Math.floor(this.score);
                let half = Math.floor(this.score % 1 * 2);
                let none = STAR_LEN - full - half;
                for (let i = 0; i < full; i++) {
                    result.push('fullStar');
                };
                 for (let i = 0; i < half; i++) {
                    result.push('halfStar');
                };
                 for (let i = 0; i < none; i++) {
                    result.push('noneStar');
                };
                return result;
            }
        }
    };
</script>

<style>
    .star_wrap{
        font-size: 0;
        display: inline-block;
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
</style> 
