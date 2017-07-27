<template>
	<div class="ratings">
		<div class="ratings_div">
			<vratingSelect v-bind:ratings="ratings" v-bind:foodChoiceType="foodChoiceType"></vratingSelect>
		</div>
	</div>
</template>

<script type='text/ecmascript-6'>
	import ratingSelect from '../ratingSelect/ratingSelect';
	export default {
        data () {
            return {
                ratings: [],
                foodChoiceType: ['全部', '满意', '不满意']
            };
        },
        created () {
            this.$http.get('/api/ratings').then((response) => {
                this.ratings = response.data.data;
            });
        },
        components: {
            vratingSelect: ratingSelect
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
</style> 
