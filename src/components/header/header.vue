<template>
	<div class="header">{{ seller }}</div>
</template>

<script type='text/ecmascript-6'>
	export default {
        props: {
            seller: {
                type: Object
            }
        }
	};
</script>

<style>
	.header{
		width:100%;
		height: 50px;
		background: red;
	}
</style> 
