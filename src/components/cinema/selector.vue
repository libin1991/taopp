<template>
  	<div class="selector" v-if='selector'>
   		<div class="selector-box">
	   		<div class="selector-container">
	   			<h3 class="selector-title"><span class="selector-name">区域</span><span class="selector-sel" :class='{addColor : (localtionSel!="不限")}'>{{localtionSel}}</span></h3>
	   			<div class="selector-main">
	   				<p @click='localtionEvent($event)' v-for='reginName in selector.regionNames' >{{reginName}}</p>
	   			</div>
	   		</div>
	   		<div class="selector-container">
	   			<h3 class="selector-title"><span class="selector-name">特色</span><span class="selector-sel" :class='{addColor : (specalSel!="不限")}'>{{specalSel}}</span></h3>
	   			<div class="selector-main">
	   				<p @click='specalEvent($event)' v-for='support in selector.supports' data-id='support.supportCode'>{{support.desc}}</p>
	   			</div>
	   		</div>
	   		<div class="selector-container">
	   			<h3 class="selector-title"><span class="selector-name">时段</span><span class="selector-sel" :class='{addColor : (timeSel!="不限")}'>{{timeSel}}</span></h3>
	   			<div class="selector-main">
	   				<p @click='timeEvent($event)' v-for='time in selector.timeMap' data-id='time.timeRange'>{{time.desc}}</p>
	   			</div>
	   		</div>
   		</div>
		<div class="btn-group">     
			<button @click='closeSelector' class="cancel-btn" data-tap="1">取消筛选</button>     
			<button class="confirm-btn" data-tap="1">确定</button>  
		</div>

  </div>
</template>

<script>
export default {
	data(){
		return{
			localtionSel:'不限',
			specalSel : '不限',
			timeSel : '不限',
		}
	},
	methods:{
		localtionEvent(event){

			if(this.localtionSel != event.target.innerHTML){
				this.localtionSel = event.target.innerHTML;
				event.target.className = 'addColor2';
			}else{
				this.localtionSel = '不限';
			}
		},
		specalEvent(event){
			this.specalSel = event.target.innerHTML;
		},
		timeEvent(event){
			this.timeSel = event.target.innerHTML;
		},
		closeSelector(){
			this.$parent.isSelector = false;
		}
	},
	props:['selector'],
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" rel="stylesheet/stylus" scoped>
@import '../../common/css/transition.styl';
.selector
	position:fixed;
	left:0;
	top:41px;
	bottom:0px;
	overflow:auto;
	background-color:#fff;
	z-index:11;
	.selector-box
		 padding-bottom: 4rem;
	.btn-group{
		height:4rem;
	    width:100%;
	    position:fixed;
	    background-color:#fff;
	    bottom:0;
	    left:0;
	    padding:0 15px;
	    border-top:1px solid #ddd;
	    width:100%;
	    box-sizing:border-box;
	    z-index:11;
	    display:flex;
	    align-items:center;
	    justify-content:space-between;
	    .cancel-btn,.confirm-btn{
			width:45%;
			text-align:center;
			line-height:2.8rem;
			height:2.8rem;
			border-radius:5px;
			font-size:1rem;
			border:0;
			background-color:#fff;
			color:#888;
			font-size:1rem;
			font-family: 'PingFang SC','STHeitiSC-Light',"Microsoft YaHei",Arial,"Helvetica Neue",Helvetica,sans-serif;
		}
		.cancel-btn{
			border:1px solid #888;
		}
   		.confirm-btn{
			background-color:$color;
			color:#fff;
   		}
	}
	.selector-container
		padding-left:15px;
		margin-top:5px;
		.selector-title
			line-height:2.5rem;
			.selector-name
				font-size:.9rem;
				font-weight:bold;
			.selector-sel
				font-size:0.725rem;
				margin-left:8px;
				color:#888;
			.addColor
				color:$color;
		.selector-main
			padding-bottom:5px;
			border-bottom:1px solid #ddd;
			p
				width:22.5%;
				height:2.2rem;
				line-height:2.2rem;
				color:#888;
				border:1px solid #ddd;
				border-right:0;
				box-sizing:border-box;
				margin-right:2%;
				text-align:center;
				margin-bottom:0.7rem;
				display:inline-block;
			.addColor2
				color:$color;
				border-color:$color;
		&:last-child .selector-main
			border:0;
</style>
