<template>
	<div>
				<mytransfer :sourcedata="gameList" :targetdata="checkedGame" @rightMove="handleRightChange" @leftMove="handleLeftChange"></mytransfer>		
	</div>
</template>

<script>
	import mytransfer from './mytransfer.vue'
	export default {
		components: {
			mytransfer
		},
		data() {
			return {
				checkedGame: [],
				gameList: [],
			}
		},
		methods: {
			handleRightChange(pid) {
				
			},
			handleLeftChange(pid) {
				
			}
		}
	}
</script>

<style>
	
</style>