<template>
	<div class="container slide2" id="Work">
	<div id="counter">{{constants.dis}}</div>
		<div class="row">
			<div class="description">
				<section v-for="desc in description">
					<h1>{{desc.title}}</h1>
					<p>{{desc.tag}}</p>
					<span id="spam">{{message}}, {{constants}}</span>here?
				</section>
			</div>
			<div id="carousel-wrap" :style="stickyWrap">
				<div id="carousel" :style="rotateObject">
					<figure v-for="car in carousel">
						<div class="frame" v-on:click="car.show = !car.show">
							<!-- <transition name="fade"> -->
								<img v-if="!car.show" :src="car.imgUrl">
								<iframe v-if="car.show" :src="car.frameUrl"></iframe>
							<!-- </transition> -->
							<!-- <transition name="fade"> v-show="car.cover"-->
							<div class="frame-cover" :class="{ hideCover: !car.cover }"></div>
							<!-- </transition> -->
						</div>
					</figure>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default{
	name:'slide2',
	props:['message'],
	data () {
		return{
			description:[{
				title: 'Sylvan Esso',
				tag:'This site is great.  I made it.  It\'s very simple.  That\'s cool',
				details:''
			},{
				title: 'Day in the Life',
				tag:'Here is a SPA web app I wrote once upon a time.',
				details:''
			},{
				title: 'Bar Virgile',
				tag:'A website made for a Restaurant/Bar located in downtown Durham, NC',
				details:''

			},{
				title: 'Sylvan Esso',
				tag:'',
				details:''

			},{
				title: 'Sylvan Esso',
				tag:'',
				details:''

			},{
				title: 'Sylvan Esso',
				tag:'',
				details:''

			}],
			carousel:[{
				show:false,
				cover:true,
				imgUrl:"src/img/sites/SE_full.jpg",
				frameUrl:"http://www.sylvanesso.com/"

			},{
				show:false,
				cover:true,
				imgUrl:"src/img/sites/ditl_full.jpg",
				frameUrl:""

			},{
				show:false,
				cover:true,
				imgUrl:"",
				frameUrl:""

			},{
				show:false,
				cover:true,
				imgUrl:"",
				frameUrl:""

			},{
				show:false,
				cover:true,
				imgUrl:"src/img/sites/BV_full.jpg",
				frameUrl:"http://internestcollective.com/barvirgile/menus/"

			},{
				show:false,
				cover:true,
				imgUrl:"src/img/sites/ditl_full.jpg",
				frameUrl:"http://bowerbirds.org/"

			}],
			constants:{
				winHeight: window.innerHeight,
				direction: 0,
				dis: ''


			},
			rotateObject:{}
		}
	},
	watch: {
		message: function(){
			this.rotateCarousel()
		}
	},
	methods: {
		rotateCarousel: //_.debounce( 
			function () {

				var rungs = this.constants.winHeight,
					rungHeight = Math.round(this.message % rungs),
					winScroll = this.message - (this.constants.winHeight),
					whichRung = Math.ceil((winScroll / rungs) - 0.2);

					this.constants.dis = Math.ceil((winScroll / rungs) - 0.2)//Math.abs(whichRung - 6) ;
				// document.getElementById("counter").html('whichRung');	

				if(winScroll > 0 && winScroll < (rungs * 5.1)){
					this.stickyWrap = {
						position:'fixed'
					}



					if( this.constants.direction - this.message < 0){

						if(rungHeight > (this.constants.winHeight * 0.2)){
							this.rotateObject = {
								transition:'transform 1.5s',
								transform:'rotateX('+Math.round((whichRung * 60))+'deg)'
							}
							for(var i = 0; i < 6; i++){
								this.carousel[i].cover = true
							}
						}
						// if(rungHeight <= this.constants.winHeight/2){
						// 	this.rotateObject = {
						// 		transition:'transform 0.1s',
						// 		transform:'rotateX('+Math.round((winScroll)*(60/rungs))+'deg)'
						// 	}
						// }else{
						else if(rungHeight > 0 && rungHeight < (this.constants.winHeight * 0.2)){

							
							for(var i = 0; i < 6; i++){
								if (i != Math.abs(whichRung - 6)){
									this.carousel[i].cover = true
								}else{
									this.carousel[Math.abs(whichRung - 6)].cover = false
								}

							}
						}
					}else{
						if(rungHeight < (this.constants.winHeight * 0.2) ){
							this.rotateObject = {
									transition:'transform 1.5s',
									transform:'rotateX('+Math.round((whichRung - 1) * 60)+'deg)'
								}
						}
						// if(rungHeight > this.constants.winHeight/2){
						// 	this.rotateObject = {
						// 		transition:'transform 0.3s',
						// 		transform:'rotateX('+Math.round((winScroll)*(60/rungs))+'deg)'
						// 	}
						// }else{
						// 	this.rotateObject = {
						// 		transition:'transform 1s',
						// 		transform:'rotateX('+Math.round((whichRung - 1) * 60)+'deg)'
						// 	}
						// }
					}
				}else if(winScroll >= (rungs * 5.1)){

					this.stickyWrap = {
						position:'absolute',
						top:(560) + 'vh'
					}

					// this.rotateObject = {
					// 	transition:'transform 0.06s',
					// 	transform: 'rotateX('+((5) * 60)+'deg) translate3d(0,0,-'+((winScroll - (this.constants.winHeight*5)))+'px )' ///Y part -'+(0.5*(winScroll - (this.constants.winHeight*5)))+'px
					// }
				}else{

					this.stickyWrap = {
						position:'absolute'
					}

					// this.rotateObject = {
					// 	transition:'none',
					// 	transform:'translateY('+Math.abs(winScroll)+'px)'
					// }
				}

				this.constants.direction = this.message
			} 
			//, 450 );
		
	}
}
</script>
<style lang="sass">
	.fade-enter-active, .fade-leave-active {
  transition: opacity .5s
}
.fade-enter, .fade-leave-to /* .fade-leave-active in <2.1.8 */ {
  opacity: 0;
}



/* work 
------------------------------------------------- */
.slide2{
  color:#fff;
  background:#4a4a4a;
  /*background: -webkit-linear-gradient(left,#333,#4a4a4a 10%, #4a4a4a 80%, #333 96%);
  background: -o-linear-gradient(left,#333,#4a4a4a 10%, #4a4a4a 80%, #333 96%);
  background: -moz-linear-gradient(left,#333,#4a4a4a 10%, #4a4a4a 80%, #333 96%);
  background: linear-gradient(to right, #333,#4a4a4a 10%, #4a4a4a 80%, #333 96%);*/
  height:600vh;

  	.row{
  		position:relative;
  	}

	section{
	  position:relative;
	  z-index:3;
	  height:100vh;
	}
	/*#carousel-wrap::after{
		content:'';
		position:fixed;
		background: linear-gradient(to bottom, rgba(74,74,74,1) 80%, transparent 100%);
		transform:translate3d(-80vh,-48vh,1vh);
		width:150%;
		height:30vh;
	}*/
	/*#carousel-wrap::before{
		content:'';
		position:fixed;
		background: linear-gradient(to top, rgba(74,74,74,1) 70%, transparent 100%);
		transform:translate3d(-80vh,39vh,1vh);
		width:150%;
		height:20vh;
		z-index:4;
	}*/
	#carousel-wrap{
	  position:absolute;
	  top:50vh;
	  left:10vw;
	  width:80vw;
	  height:80vh;
	  z-index:2;
	  -webkit-perspective:1000px; 
	  perspective: 1000px;

		#carousel{
		  position: absolute;
		  width:40vw;
		  height:40vh;
		  transform-style: preserve-3d;
		  /*transform:rotateX(0deg) translateY(100vh);*/

			figure{
			  border:1px solid #333;
			  display:block;
			  position:absolute;
			  width:40vw;
			  height:40vh;
			  left:20vw;
			  margin:0;
			  padding:0;
			  overflow:hidden;
			  -webkit-backface-visibility: hidden;
			  backface-visibility: hidden;
			}
			figure:nth-child(1){
			  transform:rotateX(0deg) translate3d(0,0,34.64vh); 
			}
			figure:nth-child(2){
			  transform:rotateX(60deg) translate3d(0,0,34.64vh);
			}
			figure:nth-child(3){
			  transform:rotateX(120deg) translate3d(0,0,34.64vh); 
			}
			figure:nth-child(4){
			  transform:rotateX(180deg) translate3d(0,0,34.64vh); 
			}
			figure:nth-child(5){
			  transform:rotateX(240deg) translate3d(0,0,34.64vh); 
			}
			figure:nth-child(6){
			  transform:rotateX(300deg) translate3d(0,0,34.64vh); 
			}

			iframe{
			  position:relative;
			  border:none;
			  width:200%;
			  height:80vh;
			  -webkit-backface-visibility: hidden;
			  backface-visibility: hidden;
			  -ms-zoom: 0.5;
			  -moz-transform: scale(0.5);
			  -moz-transform-origin: 0 0;
			  -o-transform: scale(0.5);
			  -o-transform-origin: 0 0;
			  -webkit-transform: scale(0.5);
			  -webkit-transform-origin: 0 0;
			}
			img{
			  width:100%;
			}
			.frame-cover{
			  position:absolute;
			  top:0;
			  left:0;
			  width:100%;
			  height:80vh;
			  background:rgba(0,0,0,0.7);
			  opacity:1;
			  visibility:visible;
			  transition:opacity 0.7s, visibility 0.7s;
			}
			.hideCover{
				opacity: 0;
				visibility:hidden;
			}
			h2{
			  font-size:14px;
			  letter-spacing: 0.4em;
			  text-transform:uppercase;
			  margin:10px 0 22px;
			  text-align:left;
			  font-style: italic;
			}
			.frame-hide{
			  opacity:0;
			  visibility:hidden;
			}
		}
	}
}
#counter{
	position:fixed;
	left:20px;
	top:50px;
}

</style>