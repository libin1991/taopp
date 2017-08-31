<template>
  <div class="movie remove-nav">
   		<div class="movie-header clearfix">
   			<img class="left logo" src="./img/logo.png" alt="">
   			<div class="left movie-localtion overflow-text" @click='showSelect()'>
   				{{localtion}}
   			</div>
        <div class="right f0">
                <router-link to='/movie' class="hot-screen">正在热映</router-link>
                <router-link to='/movie/begin' class="begin-screen">即将上映</router-link>
          </div> 
   		</div>
      <transition name='move'>
        <router-view></router-view>
      </transition>
       <transition name='move'>
          <selectcity v-show='isSelect'></selectcity>
       </transition>
  </div>
</template>

<script>
import selectcity from '@/components/selectcity/selectcity';
export default {
  data () {
  	return {
  		localtion:'北京',
      isSelect : false,
  	}
  },
  methods : {
      showSelect(){
          this.isSelect = true;
      }
  },
  components:{selectcity},
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" rel="stylesheet/stylus" scoped>
@import '../../common/css/transition.styl';
.t-c{
  text-align:center;
}
.movie
	color:#595757;
	.movie-header
		height:40px;
		.logo
			padding:2px;
			height:22px;
			width:22px;
			border-radius:4px;
			background:#90B4FC;
			margin:7px 15px;
		.movie-localtion{
        max-width:70px;
        display:inline-block;
        line-height:40px;
        padding-right:18px;
        background:url('./img/down.png') no-repeat right center;
        background-size:12px auto;
    }
		.hot-screen,.begin-screen{
			margion-top:2px;
			padding:12px 15px;
			display:inline-block;
			font-size:0.875rem;
			&.router-link-exact-active{
				border-bottom:2px solid $color;
				color : $color;
			}
		}
</style>
