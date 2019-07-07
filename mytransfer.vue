<template>
	<div class="whole-component">
		<div class="left-container">
			<el-radio-group v-model="temPid" class="radio-group">
				<el-radio v-for="item in sourcedata" :key="item.pid" v-model="item.pid" :label="item.pid" class="radio-self">{{item.gameName}}</el-radio>
			</el-radio-group>
		</div>
		<div class="move-button-group">
			<el-button type="primary" icon="el-icon-arrow-left" circle class="move-button" @click="leftMove"></el-button>
			<el-button type="primary" icon="el-icon-arrow-right" circle class="move-button" @click="rightMove"></el-button>
		</div>
		<div class="right-container">
			<el-radio-group v-model="rightTemPid" class="checkbox-group" @change="opFlagChange">
				<el-radio :label="titem.pid" v-for="titem in targetdata" :key="titem.pid" v-model="titem.pid" class="checkbox-self">{{titem.gameName}}</el-radio>
			</el-radio-group>
		</div>
		<div class="move-up-down-gourp">
			<el-button type="primary" icon="el-icon-arrow-up" circle class="move-button" @click="upMove" :disabled="opFlag"></el-button>
			<el-button type="primary" icon="el-icon-arrow-down" circle class="move-button" @click="downMove" :disabled="opFlag"></el-button>
		</div>
	</div>
</template>

<script>
	export default {
		props: ['sourcedata', 'targetdata'],
		create() {
			
		},
		data() {
			return {
				temPid: '',
				rightTemPid: '',
				opFlag: true
			}
		},
		methods: {
			leftMove() {
				for(let index in this.targetdata) {
					let game = this.targetdata[index];
					if(game.pid == this.rightTemPid) {
						this.sourcedata.push(game);
						this.targetdata.splice(index, 1);
						this.$emit('leftMove', game.pid);
					}
				}
			},
			rightMove() {
				for(let index in this.sourcedata) {
					let game = this.sourcedata[index];
					if(game.pid == this.temPid) {
						this.targetdata.push(game);
						this.sourcedata.splice(index, 1);
						this.$emit('rightMove', game.pid);
					}
				}
			},
			upMove() {
				//保存被选中的下标
				let $index = 0;
				for(let index in this.targetdata) {
					let game = this.targetdata[index];
					if(this.rightTemPid == game.pid) {
						$index = index;
					}
				}
				if($index == 0) {
					return
				}
				this.swapItems(this.targetdata, $index, $index - 1);

			},
			downMove() {
				//保存被选中的下标
				let vindex = 0;
				for(let index in this.targetdata) {
					let game = this.targetdata[index];
					if(this.rightTemPid == game.pid) {
						vindex = index;
					}
				}
				if(vindex == this.targetdata.length - 1) {
					return
				}
				this.swapItems(this.targetdata, vindex++, vindex);
			},
			opFlagChange() {
				this.opFlag = false;
			},
			swapItems(arr, index1, index2) { //数组元素换位
				arr[index1] = arr.splice(index2, 1, arr[index1])[0];
				return arr;
			}
		}
	}
</script>

<style>
	.whole-component {
		display: flex;
		justify-content: space-between;
		width: 500px;
		margin-top: 20px;
	}
	/*overflow:auto;超出后显示滚动条*/
	
	.left-container {
		width: 185.4px;
		height: 300px;
		border: 1px solid #CCCCCC;
		overflow: auto;
	}
	
	.right-container {
		width: 185.4px;
		height: 300px;
		border: 1px solid #CCCCCC;
		overflow: auto;
	}
	
	.move-button-group {
		display: flex;
		flex-direction: column;
		justify-content: center;
	}
	
	.move-up-down-gourp {
		display: flex;
		flex-direction: column;
		justify-content: center;
	}
	/*margin-top: 10px覆写了el-button默认的margin*/
	
	.move-button {
		width: 40px;
		height: 40px;
		margin-top: 10px;
	}
	
	.radio-group {
		display: flex;
		flex-direction: column;
		width: 100%;
		height: 100%;
	}
	
	.radio-self {
		margin: 10px 5px;
	}
	
	.checkbox-self {
		margin: 10px 5px;
	}
	
	.checkbox-group {
		display: flex;
		flex-direction: column;
		width: 100%;
		height: 100%;
	}
</style>