<template>
	<div class="shopBtn">
        <span v-on:click="item_plus()" class="item_a item_plus">+</span>
        <span v-if="num"  class="choice_num">{{num}}</span>
        <span v-if="num" v-on:click="item_reduce()"  class="item_a item_reduce">-</span>
	</div>
</template>

<script type='text/ecmascript-6'>
	export default {
        props: {
            itemNum: {
                type: Number,
                default: 0
            }
        },
        data () {
            return {
                num: this.itemNum
            };
        },
        watch: {
            itemNum (val) {
                this.num = val;
            }
        },
        methods: {
            item_plus (e) {
                if (this.num >= 0) {
                    this.num ++;
                    this.$emit('clickPlus');
                } else {
                    return false;
                }
            },
            item_reduce (e) {
                if (this.num >= 0) {
                    this.num --;
                    this.$emit('clickReduce');
                    this.$emit('detailClickReduce');
                } else {
                    return false;
                }
            }
        }
	};
</script>
<style>
	.shopBtn{
        display: inline-block;
        float: right;
	}
    .item_a{
        float: right;
        display: inline-block;
        font-size:20px;
        width: 20px;
        height:20px;
        line-height: 16px;
        text-align: center;
        border:2px solid #008fe1;
        border-radius:50%;
        font-weight: bold;
    }

    .item_reduce{
        color:#008fe1;
        background-color:#fff;
    }
    .item_plus{
        color:#fff;
        background-color:#008fe1;
        margin-right: 6px;
    }
    .choice_num{
        line-height: 24px;
        font-size:16px;
        margin:0 8px;
        float: right;
        display: inline-block;
        color:grey;
    }
</style>
