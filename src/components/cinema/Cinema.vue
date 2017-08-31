<template>
  	<div class="cinema remove-nav">
   		<div class="cinema-header clearfix">
   		  <selectcity></selectcity>
        <div class="right f0">
                <p @click='selector' :class='{selector:isSelector}' class="hot-screen">筛选</p>
                <p class="begin-screen">搜索</p>
          </div> 
   		</div>
        <transition name='move'>
        	<selector v-show='isSelector' :selector='cinemaList.cinemaFilter'></selector>
        </transition>
  </div>
</template>

<script>
	import selectcity from '@/components/selectcity/selectcity';
	import selector from '@/components/cinema/selector';
	export default {
	  data(){
	  	return {
	  		isSelector : false,
	  		cinemaList : '',
	  	}
	  },
	  components:{selectcity,selector},
	  methods : {
	  	selector(){
	  		this.isSelector = true;
	  	},
	  },
	  created(){
       this.$http.get('/api/cinema').then((response) => {
            response = response.body;
            if(response.data.returnCode == 0){
              this.cinemaList = response.data.returnValue;
              console.log(this.cinemaList)
            }
         });
      },
	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" rel="stylesheet/stylus" scoped>
@import '../../common/css/transition.styl';
.t-c{
  text-align:center;
}
.cinema
	color:#595757;
	.cinema-header
		height:40px;
		border-bottom:1px solid #ddd;
		.hot-screen,.begin-screen{
			margion-top:2px;
			padding:2px 10px 2px 20px;
			display:inline-block;
			font-size:0.875rem;
			margin-top:10px;
			display:inline-block;
		}
		.hot-screen
			background:url('./img/selector.png') no-repeat left center;
			background-size:1rem;
		.begin-screen
			background:url('./img/search.png') no-repeat 5px center;
			background-size:1.2rem;
			padding-left:25px;
			border-left:1px solid #ddd;
		.selector
			color:$color;
			background-image:url('./img/selector2.png');
</style>
