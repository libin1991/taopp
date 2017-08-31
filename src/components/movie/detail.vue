<template>
	<div id="detail" class="detail remove-nav">
		<div class="detail-msg">
			<div class="detail-msg-info">
				<img v-if='!!movieProject.poster' class="detail-msg-img" :src="'//gw.alicdn.com/'+movieProject.poster+'_400x400Q30s150.jpg'" alt="">
				<div class="detail-msg-box">
					<p class="showName"><span class="showName-title">{{movieProject.showName}}</span><span class="showName-icon" v-if='!!movieProject.showMark'>{{movieProject.showMark}}</span></p>
					<p class="showNameEn">{{movieProject.showNameEn}}</p>
					<ul class="movie-msg">
						<li>{{movieProject.type}}</li>
						<li>{{movieProject.country}} | {{movieProject.duration}}分钟</li>
						<li>
							<span v-if='!!movieProject.features'>{{movieProject.features.openTime}}</span>
							<span v-if='!!movieProject.features'>在{{movieProject.features.openCountry}}上映</span>
						</li>
						<li><span>想看人数</span></li>
						<li><span class="wantCount">{{movieProject.wantCount}}</span></li>
					</ul>
				</div>
			</div>
		</div>
		<div class="movie-desc">
			<p v-html='description(desc,descStrNum)'></p>	
			<p @click='descBtnClick' class="desc-btn">{{descBtn ? '展开' : '收起'}}</p>
		</div>
		<_line></_line>
		<div class="movie-artist-list">
			<p class="movie-artist-title">剧照</p>
			<div class="pics" id="picDom">
                <ul class="pics-list" id="picsList">
                    <li class="pics-item"  v-for='artist in movieProject.trailer'>
                      <img :src="'//gw.alicdn.com/'+artist+'_160x160Q30s150.jpg'"  height="102" width="74" alt=""/>
                    </li>
                </ul>
            </div>
		</div>
	</div>
</template>
<script>
	import BScroll from 'better-scroll';
	import _line from '@/components/line/line';
	export default{
		data(){
			return {
				desc :'<span style="color:#f00">这块数据JSON里面没有，所以是固定的</span> 故事改编自著名的二战军事事件“敦刻尔克大撤退”。二战初期，40万的英法盟军被敌军围困于敦刻尔克的海滩之上，面对敌军步步逼近的绝境，他们不得不为自己的命运背水一战，才有可能活着回家。 本片以二战时期代号为“发电机计划”的敦刻尔克大撤退为故事背景，是一部从不同视角聚焦人类生存的电影。影片将会分成沙滩上的步兵部分（芬恩·怀特海德与哈里·斯泰尔斯参演）、海军部分（希里安·墨菲与马克·里朗斯参演）以及空军部分（汤姆·哈迪开战斗机）分别来讲述，力求从不同的个人观点来呈现和构建这起历史事件。',
				descBtn : true,
				descStrNum : 100
			}
		},
		props:['movieProject'],
		watch:{
			movieProject:function(val,oldval){
				console.log(val,oldval)
			}
		},
		methods:{
			description(str,num){
				if(num){
					return str.substr(0,num)+"...";
				}
				return str;
			},
			descBtnClick(){
				this.descBtn = !this.descBtn;
				this.descStrNum = !!this.descStrNum ? 0 : 100;
			},
     		 _initPic(){
		        if (this.movieProject.trailer) {
		          let picWidth = 74;
		          let margin = 6;
		          let width = (picWidth + margin) * this.movieProject.trailer.length - margin;
		          picsList.style.width = width + 'px';
		          this.$nextTick(()=>{
		            if(!this.picScroll){
		              this.picScroll = new BScroll(picDom, {
		                scrollX: true,
		                //eventPassthrough: 'vertical'
		              })
		            }else{ 
		              this.picScroll.refresh();
		            }
		          })
		        }
      		},
		},
		mounted(){
	      this._initPic();
	    },
	    updated(){
	      this._initPic();
	    },
		components:{_line},
	}
</script>
<style lang="stylus" rel="stylesheet/stylus" scoped>
@import '../../common/css/transition.styl';
	.detail
		position:fixed;
		height:100%;
		width:100%;
		left:0;
		top:0;
		background:#fff;
		overflow:auto;
		.detail-msg
			position:relative;
			background:#333;
			padding-top:25px;
			height:200px;
		.detail-msg-img
			width:120px;
			padding:0 15px;
			position:absolute;
			left:0;
			top:30px;
		.detail-msg-box


			padding-left:150px;
			box-sizing:border-box;
			text-align:left;
			.showName
				display:flex;
				align-item:center;
				margin-top:12px;
				.showName-title
					font-size:1.1rem;
					color:#fff;
				.showName-icon
					font-size:10px;
					border-radius:3px;
					padding:0 2px;
					line-height:16px;
					border:1px solid #aaa;
					color:#aaa;
					margin-left:10px;
			.showNameEn
				font-size:0.75rem;
				color:#fff;
				margin-top:7px;
			.movie-msg
				margin-top:30px;
				li
					font-size:0.75rem;
					color:#eee;
					margin-top:7px;
					.wantCount
						color:#ffa84c;
						font-size:1.125rem;
		.movie-desc{
		    font-size:0.8rem;
		    line-height:25px;
		    text-align:left;
			padding:0 15px;
		    color:#333;
		    margin:20px 0;
		}
		.desc-btn{
			text-align:center;
			color:$color;
			font-size:1rem;
			padding-top:15px;
		}
		.movie-artist-list{
			padding-left:15px;
			.movie-artist-title{
				color:#333;
				font-weight:700;
				font-size:1;
				text-align:left;
				padding:15px 0;
			}
			.artist-photo{
				display:inline-block;
				width:74px;
				height:102px;
			}
			.pics{
	            padding-bottom:18px;
	            overflow:hidden;
	            .pics-list{
	              white-space:nowrap;
	              font-size:0;
	              .pics-item{
	                display: inline-block;
	                margin-right:6px;
	                &:last-child{
	                  margin-right:0;
	                 }
	              }
	            }
	          }
		}
</style>