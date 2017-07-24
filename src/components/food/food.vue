<template>
	<div class="food">
		<span class="back" v-on:click="back"></span>
        <div class="head_pic_wrap">
            <img v-bind:src="food.image" alt="">
        </div>
	</div>
</template>

<script type='text/ecmascript-6'>
    export default {
        props: {
            food: {
                type: Object
            }
        },
        methods: {
            back () {
                this.$emit('backTo');
            }
        }
    };
</script>

<style>
	.food{
        width:100%;
        height:100%;
        background:#fff;
        position:fixed;
        top:0;
        left:0;
        bottom:54px;
    }
    .back{
        display: block;
        width:15px;
        height:32px;
        color:#fff;
        background:url(./images/back.png) no-repeat center center;
        background-size: 15px 32px;
        position: absolute;
        left:20px;
        top:20px;
        z-index:999;
    }
    .head_pic_wrap{
        width:100%;
        padding-top:100%;
    }
    .head_pic_wrap img{
        position:absolute;
        left:0;
        top:0;
        width:100%;
    }
</style>
