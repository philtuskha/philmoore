<template>
	<div class="container slide2" id="Work">
	<div id="counter">{{constants.dis}}</div>
		<div class="row">
			<div class="description">
				<section v-for="(desc, index) in description">
					<h1>{{desc.title}}</h1>
					<p class="tag">{{desc.tag}}</p>
					<!-- <p class="description" :class="{ hideP: !carousel[indexCheck(index)].cover }">{{desc.details}}</p> :class="{ hideCover: !carousel[index].cover }" -->
				</section>
			</div>
			<div id="karousel-wrap" :style="stickyWrap">

				<div id="karousel" :style="rotateObject">
					<figure v-for="car in carousel">
						<div class="frame" v-on:click="car.show = !car.show">
							<transition name="fade">
								<img v-if="!car.show" :src="car.imgUrl">
								<iframe v-if="car.show" :src="car.frameUrl"></iframe>
							</transition>
							<div class="frame-cover" :class="{ hideCover: !car.cover }"></div>
						</div>
					</figure>
				</div>
				<h1>Sylvan Esso</h1>
			</div>
		</div>
	</div>
</template>

<script>
import _ from 'lodash'

export default{
	name:'slide2',
	props:['message'],
	data () {
		return{
			description:[{
				title: 'Sylvan Esso',
				tag:'This site is great.  I made it.  It\'s very simple.  That\'s cool',
				details:'Here some ver important details.  I\m excited to have made this site.  Now I can show all my friends the great stuff that I own forever.  You break it you buy it!'
			},{
				title: 'Day in the Life',
				tag:'Here is a SPA web app I wrote once upon a time.',
				details:'Here some ver important details.  I\m excited to have made this site.  Now I can show all my friends the great stuff that I own forever.  You break it you buy it!'
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
			rotateObject:{},
			stickyWrap:{}
		}
	},
	watch: {
		message: function(){
			this.stickyCarosuel()
		}
	},
	methods: {
		indexCheck: function(i){
			var realIndex = i == 0 ? 0 : 6 - i
			return realIndex
		},
		coverReset: function(ar){
			var c = this.carousel;
			if(ar != null){
				for(var i = 0; i < 6; i++){
					if (i != ar){
						c[i].cover = true
						c[i].show = false
					}else{
						c[ar].cover = false

					}
				}
			}else{
				for(var i = 0; i < 6; i++){
					c[i].cover = true

				}
			}
		},
		stickyCarosuel: function(){

			var rungs = this.constants.winHeight,
				winScroll = this.message - (this.constants.winHeight);

			if(winScroll > 0 && winScroll < (rungs * 5.1)){
				this.stickyWrap = {
					position:'fixed',
				}

				this.rotateCarousel()


			}else if(winScroll >= (rungs * 5.1)){
				this.rotateObject = {
					transition:'transform 1.5s',
					transform:'rotateX(300deg)'
				}

				this.stickyWrap = {
					position:'absolute',
					top:(560) + 'vh'
				}
			}else{

				this.rotateObject = {
					transition:'transform 1.5s',
					transform:'rotateX(0deg)'
				}

				this.stickyWrap = {
					position:'absolute'
				}
				this.coverReset(null)
				
			}

		},
		rotateCarousel: _.debounce( function () {

				var rungs = this.constants.winHeight,
					rungHeight = Math.round((this.message - (rungs * 0.2)) % rungs),
					winScroll = this.message - (this.constants.winHeight),
					whichRung = Math.ceil((winScroll / rungs) - 0.2),
					adjustedRung = Math.abs(whichRung - 6) % 6;
					

				// function coverReset(ar){
				// 	console.log(ar != null)
				// 	if(ar != null){
				// 		for(var i = 0; i < 6; i++){
				// 			if (i != ar){
				// 				c[i].cover = true
				// 				c[i].show = false
				// 			}else{
				// 				c[ar].cover = false
				// 			}
				// 		}

				// 	}else{
				// 		for(var i = 0; i < 6; i++){
				// 			c[i].cover = true
				// 		}

				// 	}
				// }

				///for build purposes
				//this.constants.dis =  this.carousel[0].cover + ' : ' + rungHeight + ' : ' + this.constants.winHeight * 0.8 + ' : ' + adjustedRung

				// if(winScroll > 0 && winScroll < (rungs * 5.1)){
				// 	this.stickyWrap = {
				// 		position:'fixed'
				// 	}

					if( this.constants.direction - this.message < 0){

						if(rungHeight > 0 && rungHeight < (this.constants.winHeight * 0.8)){
							this.rotateObject = {
								transition:'transform 1.5s',
								transform:'rotateX('+Math.round((whichRung * 60))+'deg)'
							}

							this.coverReset(null)

						}else{

							this.coverReset(adjustedRung)
							
						}
					}else{
						if(rungHeight > 0 && rungHeight < (this.constants.winHeight * 0.8)){

							this.coverReset(null)

						}else{
							this.rotateObject = {
									transition:'transform 1.5s',
									transform:'rotateX('+Math.round((whichRung) * 60)+'deg)'
								}
							
							this.coverReset(adjustedRung)

						}
					}
				// }else if(winScroll >= (rungs * 5.1)){
				// 	this.rotateObject = {
				// 		transition:'transform 1.5s',
				// 		transform:'rotateX(300deg)'
				// 	}

				// 	this.stickyWrap = {
				// 		position:'absolute',
				// 		top:(560) + 'vh'
				// 	}

				// }else{
				// 	this.rotateObject = {
				// 		transition:'transform 1.5s',
				// 		transform:'rotateX(0deg)'
				// 	}

				// 	this.stickyWrap = {
				// 		position:'absolute'
				// 	}
				// 	coverReset(null)
					
				// }

				this.constants.direction = this.message
			}, 0 )
		
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
  background: -webkit-linear-gradient(left,#333,#4a4a4a 10%, #4a4a4a 80%, #333 96%);
  background: -o-linear-gradient(left,#333,#4a4a4a 10%, #4a4a4a 80%, #333 96%);
  background: -moz-linear-gradient(left,#333,#4a4a4a 10%, #4a4a4a 80%, #333 96%);
  background: linear-gradient(to right, #333,#4a4a4a 10%, #4a4a4a 80%, #333 96%);
  height:600vh;

  	.row{
  		position:relative;
  	}

	section{
	  position:relative;
	  z-index:3;
	  height:100vh;
	  pointer-events: none;

	  .tag{
	  	font-size:1.4em;
	  }

	  .description{
	  	display:block;
	  	margin:10vh 0 0 12vw;
	  	width:56vw;
	  	text-align:justify;
	  	line-height: 2em;
	  	opacity:1;
	    visibility:visible;
	    transition:opacity 0.7s, visibility 0.7s;

	  }
	  .hideP{
	  	opacity:0;
		visibility:hidden;
	  }
	}
	#karousel-wrap{
	  position:absolute;
	  top:50vh;
	  left:10vw;
	  width:80vw;
	  height:80vh;
	  z-index:2;
	  -webkit-perspective:1000px; 
	  perspective: 1000px;

		#karousel{
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
			  cursor:pointer;
			}
			img{
			  width:100%;
			  cursor:pointer;
			}
			.frame-cover{
			  position:absolute;
			  top:0;
			  left:0;
			  width:105%;
			  height:80vh;
			  background:rgba(25,25,25,0.8);
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