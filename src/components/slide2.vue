<template>

	<div class="container slide2" id="/Work" rel="Work">
	<!-- <div id="counter">{{constants.dis}}</div> -->
		<div class="row">
			<div class="description">
				<section v-for="(desc, index) in description" :id=" '/Work/'+ index" :rel=" 'Work'+ index">
					<h1>{{desc.title}}</h1>
					<p class="tag">{{desc.tag}}</p>
					<!-- <p class="description" :class="{ hideP: !carousel[indexCheck(index)].cover }">{{desc.details}}</p> :class="{ hideCover: !carousel[index].cover }" -->
				</section>
			</div>
			<div id="karousel-wrap" :style="stickyWrap">
				<div id="karousel" :style="rotateObject" >
					<figure v-for="(car, index) in carousel">
						<div class="frame" v-on:click="car.show = !car.show">
							<transition name="fade">
								<img v-if="!car.show" :src="car.imgUrl">
								<iframe v-if="car.show" :src="car.frameUrl"></iframe>
							</transition>
							<div class="frame-cover" :class="{ hideCover: !car.cover }"></div>
						</div>
					</figure>
				</div>
				<div class="rotate-details" :class="{ showRotateDeets: !carousel[slideNumber].cover, showProject:readProject }">
					<div v-on:click="readProj">Project Goal</div>
					<div v-on:click="readImp">Implementation</div>
				</div>
				<div class="site-details" :class="{rotateRight: readProject, rotateLeft: readImplementation }">
					<div class="left-carousel" :class="{ showCar: !carousel[slideNumber].cover, showProject:readProject }">
						<ul>
							<li>
								<h3><span v-for="h in description[indexCheck(slideNumber)].left.headline" v-html="h"></span></h3>
								<span v-html="description[indexCheck(slideNumber)].left.item"></span>
								<p>---click to load ---></p>
							</li>
						</ul>
					</div>
					<div class="right-carousel" :class="{ showCar: !carousel[slideNumber].cover, showImplementation: readImplementation }">
						<ul>
							<li>
								<h3><span v-for="h in description[indexCheck(slideNumber)].right.headline">{{h}}</span></h3>
								<span v-html="description[indexCheck(slideNumber)].right.item"></span>
							</li>
						</ul>
					</div>
				<div>
			</div>
		</div>
	</div>
</template>

<script>
import _ from 'lodash'

export default{
	name:'slide2',
	props:['message', 'slide'],
	data () {
		return{
			description:[{
				title: 'Sylvan Esso',
				tag:'A Band From Durham, North Carolina',
				left:{
					headline:'Project Goal',
					item: '<p>Sylvan Esso needed to direct traffic to their website to showcase a new Single, <i>Radio</i>, and b-side, <i>Kick Jump Twist</i>.</p>'+
					'<p>The Band was in the middle of an album cycle, but wanted to push their brand past that of their last album cycle to be more enigmatic.  Making the website clear and easy to navigable while maintaining focus on the videos and the music therein was important.</p> <!--<h4>Challenges:</h4>-->'
				},
				right:{
					headline:'Implementation',
					item: '<p>Worked closely with the band and their team to aquire stills from the video and other assets to come up with as the overall look.</p>'+
							'<p>Worked with third party content; Youtube, Bandsintown & Shopify, to make the site easy to maintain and consistently up to date</p>'+
							'<h4>Tools:</h4><p class="tools">HTML - CSS - jQuery - Photoshop - Bandsintown Widget - Shopify Widget</p>'
				}
				
			},{
				title: 'Day in the Life',
				tag:'An annonymous, self-policing, group-texting, web-app',
				left:{
					headline:'Project Goal',
					item: '<p>To make the internet nice again, one day at a time. The concept came as a response to the multiple posting apps that focus on user profiles as a means of maintaining congeniality.</p>'+
					'<p>Believing in the common good, I wanted to build an app with a voting system maintained by users themselves that would restrict other (bad) users from posting mean stuff while maintaining complete annonymity thereby allowing a more open forum to discuss whatever comes to mind.</p>'
				},
				right:{
					headline:'Implementation',
					item: '<p>I developed a structure consisting of Profiles, Posts that last for 24hrs, Responses & Votes.  I developed a ranking system based on user activity/popularity and notifications tied to user comments</p>'+
						'<p>DITL is a spa app and therefore uses a series of ajax calls to pull in various content as it occurs.</p>'+
						'<h4>Tools:</h4><p class="tools">HTML - CSS - jQuery - Django - Illustrator - Git - Github</p>'
				}
			},{
				title: 'Bar Virgile',
				tag:'A Bar located in Downtown Durham, NC',
				left:{
					headline:'Project Goal',
					item: '<p>Bar Virgile is a beautiful and unique bar located in downtown Durham, NC specilizing in craft cocktails and delicious food</p>'+
					'<p>The owners put a lot of care into the interior design and wanted the look and feel of the website to mimic the warm, inviting atmosphere of the space itself.</p>'+
					'<p>One of the challenges with the project was keeping the consistently rotating menus up to date.</p>'
				},
				right:{
					headline:'Implementation',
					item: '<p>The owners provided photography of the interior to base the look of the site around.  The filigree was added as a frame to offset the natural boxy tendancies of the web</p>'+
						'<p>I used a javascript plugin called, \'jeditable,\' which allows for inline editing directly on the site and a simple php script to store the information to a text file.  This allowed the owners to maintain the menus and other content themselves.</p>'+
						'<h4>Tools:</h4><p class="tools">HTML - CSS - jQuery - PHP - Photoshop</p>'
				}
			},{
				title: 'Tuskha Widget',
				tag:'A music player / download using the Soundcloud API and Shopify',
				left:{
					headline:'Project Goal',
					item: '<p>An all-in-one music player that the user could stream music from and download the album without re-directing to a third party site.</p>'+
					'<p>The Soundcloud widget has limited styling and playing capabilities due to it\'s content being wrapped in an iframe.  I decided to combine the Soundcloud API and a Shopify donation widget to create a full listening/downloading experience.</p>'
				},
				right:{
					headline:'Implementation',
					item: '<p>I used Javascript to access the Soundcloud API as well as the simple play and stop functionality.  I was able to take the waveform JSON data provided to draw my own scalable / custom styled waveform using a canvas element, somewhat re-inventing the wheel, but learning a lot in the process</p>'+
						'<p>I used a hidden shopify donation widget to further enhance the user experience</p>'+
						'<h4>Tools:</h4><p class="tools">HTML - CSS - jQuery - Soundcloud API - Shopify</p>'
				}
			},
			{
				title: 'Bowerbirds',
				tag:'A band from The North Carolia Piedmont',
				left:{
					headline:'Project Goal',
					item: '<p>To make a beautiful / fully functioning website in less than 8hrs. </p>'+
					'<p>The Bowerbirds website had not been updated in over three years and had very out of date information on it.  Whoops, This is fully my bad and happens to be one of the bands that I write music for.  We needed to make an announcement about some upcoming music that we were releasing to benefit a wonderful cause and decided that it was about time.</p>'
				},
				right:{
					headline:'Implementation',
					item: '<p>Derrick Anderson, a local photographer, provided the main image of the site</p>'+
						'<p>This site uses absolutely no javascript.  Just HTML and CSS to provide all the necessary routing to our various social media platforms, webstore and management contact</p>'+
						'<h4>Tools:</h4><p class="tools">HTML - CSS</p>'
				}
			},
			{
				title: 'This Site',
				tag:'My own portfolio Site',
				left:{
					headline:'Project Goal',
					item: '<p>To make the internet nice again, one day at a time. The concept came as a response to the multiple posting apps that focus on user profiles as a means of maintaining congeniality.</p>'+
					'<p>Believing in the common good, I wanted to build an app with a voting system maintained by users themselves that would restrict other (bad) users from posting mean stuff while maintaining complete annonymity thereby allowing a more open forum to discuss whatever comes to mind.</p>'
				},
				right:{
					headline:'Implementation',
					item: '<p>I developed a structure consisting of Profiles, Posts that last for 24hrs, Responses & Votes.  I developed a ranking system based on user activity/popularity and notifications tied to user comments</p>'+
						'<p>DITL is a spa app and therefore uses a series of ajax calls to pull in various content as it occurs.</p>'+
						'<h4>Tools:</h4><p class="tools">HTML - CSS - Javascript - Vue.js - Illustrator - Git - Github - Gulp</p>'
				}
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
				direction: 0,
				// dis: ''
			},
			rotateObject:{},
			stickyWrap:{},
			slideNumber: 0,
			readProject:false,
			readImplementation:false
		}
	},
	watch: {
		message: function(){
			this.stickyCarosuel()
		},
		slide: function(){
			
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
			console.log(this.slide)
			var rungs = this.$parent._data.winHeight,
				winScroll = this.message - (this.$parent._data.slide1Height);
				//console.log(winScroll)
			// this.constants.dis = winScroll

			if(winScroll >= 0 && winScroll < (rungs * 5.1)){
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
		rotateCarousel: function () { //_.throttle( 

				var rungs = this.$parent._data.winHeight,  ///height of each section
					rungHeight = Math.round((this.message % rungs) ),  ///offset height to reset to 0 at specific point in slide to 'do stuff' (rungs * 0.2)
					winScroll = this.message - (this.$parent._data.slide1Height),  ///how far down you are scrolled - the height of slide1
					whichRung = Math.ceil((winScroll / rungs) - 0.2),  ///the slide number you are in
					adjustedRung = Math.abs(whichRung - 6) % 6;  ///the opposite slide on the carousel to make up for reverse carousel

				if( this.constants.direction - this.message < 0){

					if(rungHeight > 0){
						
						this.rotateObject = {
							transition:'transform 1.5s',
							transform:'rotateX('+Math.round((whichRung * 60))+'deg)'
						}


						console.log(rungHeight, (this.$parent._data.winHeight * 0.7))
						if(rungHeight < (this.$parent._data.winHeight * 0.7)){
							this.coverReset(null)
							this.readProject = false
							this.readImplementation = false
						}else{
							this.slideNumber = adjustedRung;
							this.coverReset(adjustedRung)
						}	

					}else{
						this.slideNumber = adjustedRung;
						this.coverReset(adjustedRung)
					}
				}else{
					console.log(rungHeight, 0,  (this.$parent._data.winHeight * 0.7))
					if(rungHeight > 0 && rungHeight < (this.$parent._data.winHeight * 0.7)){
						this.readProject = false
						this.readImplementation = false
						this.coverReset(null)

					}else{
						this.rotateObject = {
								transition:'transform 1.5s',
								transform:'rotateX('+Math.round((whichRung) * 60)+'deg)'
							}

						this.slideNumber = adjustedRung;
						this.coverReset(adjustedRung)

					}
				}

				this.constants.direction = this.message
			}, // 56 ),
		readProj: function(){
			this.readProject = true
			this.readImplementation = false
			console.log(this.rotateObject.transform)
			var r = this.rotateObject.transform.split(')')[0] + ')'
			this.rotateObject = {
				'transition':'transform 1s',
				'transform':r +' translateX(120%)'//this.rotateObject.transform + 
			}
		},
		readImp: function(){
			this.readImplementation = true
			this.readProject = false
			console.log(this.rotateObject.transform.split(')')[0])
			var r = this.rotateObject.transform.split(')')[0] + ')'
			this.rotateObject = {
				'transition':'transform 1s',
				'transform':r +' translateX(-120%)'
			}
		}
		
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

@import '../stylesheets/partials/resources';

/* work 
------------------------------------------------- */
.slide2{
  color:#fff;
  background:#4a4a4a;
  background: -webkit-linear-gradient(left,#333,#4a4a4a 10%, #4a4a4a 80%, #333 96%);
  background: -o-linear-gradient(left,#333,#4a4a4a 10%, #4a4a4a 80%, #333 96%);
  background: -moz-linear-gradient(left,#333,#4a4a4a 10%, #4a4a4a 80%, #333 96%);
  background: linear-gradient(to right, #333,#4a4a4a 10%, #4a4a4a 80%, #333 96%);
  height:630vh;

  	.row{
  		position:relative;
  		height:630vh;
  	}
  	
	section{
	  position:relative;
	  z-index:3;
	  height:100vh;
	  pointer-events: none;

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
	  left:0;
	  width:100%;
	  height:80vh;
	  z-index:2;
	  -webkit-perspective:1000px; 
	  perspective: 1000px;

	  	.rotate-details{
	  		position:absolute;
	  		top:-24vh;
	  		left:0;
	  		height:2em;
	  		width:100%;
	  		text-align:left;
	  		z-index:23;
	  		opacity:0;
	  		transition:opacity 0.5s;
	  		display:none;

	  		div{
	  			width:40vw;
	  			background:rgba(0,0,0,0.11);
	  			display:inline-block;
	  			height:1.7em;
	  			border-radius: 0 12px 12px 0;
	  			color:#706e6e;
	  			text-align:right;
	  			padding:0.4em 0.7em;
	  		}
	  		div:nth-of-type(2){
	  			float:right;
	  			border-radius: 12px 0 0 12px ; 
	  			text-align:left;
	  		}

	  	}

	  	.showRotateDeets{
	  		opacity:1;
	  	}

	  	.site-details{
	  		position:absolute;
	  		top:-18vh;
	  		left:0;
	  		width:100%;
	  		text-align:left;
	  		z-index:-1;
	  		transform-style: preserve-3d;
	  		transition:transform 1s;
	  		z-index:13;
	  		/*border:1px solid cyan;*/

	  		div{
	  			display:inline-block;
	  			opacity:0;
	  			transition:opacity 0.5s;
	  			color:#fff;
	  			padding:0;
	  			color:$grey-blue;
	  			transition:transform 1s;

	  			ul{
	  				list-style: none;
	  				padding:0;

	  				li{
	  					
	  					h3{
	  						padding:0;
	  						margin:0;
	  						/*text-transform: uppercase;*/
	  						letter-spacing: 0.12em;
						    -webkit-justify-content: space-between; /* Safari 6.1+ */
						    display: flex;
						    justify-content: space-between;
	  					}
	  					

	  					img{
	  						width:40%;
	  					}

	  					p{
	  						font-family: 'mont';
	  						text-align: left;
	  						
	  					}
	  					p.tools{
	  						font-family: 'orator';
	  						font-size:0.8em;
	  					}
	  				}
	  			}	  			
	  		}

	  		div:hover h3{
	  			color:#fff;
	  		}

		  	.left-carousel{
		  		text-align:justify;
		  		margin-left: 3%;
		  		width:16%;
		  		/*border:1px solid rgba(0,0,0,0.1);*/
		  		padding:0 16px;
		  		box-shadow: 0px 0px 10px rgba(0,0,0,0.1);
		  		
		  	}
		  	.right-carousel{
		  		text-align: justify;
		  		float:right;
		  		margin-right: 3%;
		  		width:16%;
		  		/*border:1px solid rgba(0,0,0,0.1);*/
		  		padding: 0 16px;
		  		box-shadow: 0px 0px 10px rgba(0,0,0,0.1);
		  	}
		  	.showProject{
		  		transform:rotateY(-90deg) ;
		  	}
		  	.showImplementation{
		  		transform:rotateY(90deg) ;
		  	}
		  	.showCar{
		  		opacity:1;
		  	}

		}
		.rotateLeft{
			transform:rotateY(-90deg) translateX(-80vh);
		}

		.rotateRight{
			transform:rotateY(90deg) translateX(80vh);
		}


		#karousel{
		  position: absolute;
		  width:40%;
		  height:40vh;
		  left:30%;
		  transform-style: preserve-3d;
		  /*transform:rotateX(0deg) translateY(100vh);*/

			figure{
			  border:1px solid #333;
			  display:block;
			  position:absolute;
			  width:100%;
			  height:40vh;
			  left:0;
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
			  width:200%;
			  height:80vh;
			  background:rgba(25,25,25,0.8);
			  opacity:1;
			  visibility:visible;
			  transition:opacity 0.7s, visibility 0.7s;
			  z-index:12;

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

/* tablet */
@media only screen and (min-device-width: 768px) 
and (max-device-width: 1024px){

	  
}
/* phone */
@media only screen 
  and (max-device-width: 767px){ 
  	.slide2{
	  	#karousel-wrap{
		  	#karousel{
				width:70%;
				height:40vh;
				left:15%;
			}
			.rotate-details{
				display:block;
			}
			.site-details{
		  		top:-18vh;
		  		left:-100%;
		  		width:300%;

		  		.left-carousel{
			  		margin-left: 3%;
			  		width:90vw;
			  		/*border:1px solid rgba(0,0,0,0.1);*/
			  		padding:0 16px;
		  		
			  	}
			  	.right-carousel{
			  		text-align: justify;
			  		float:right;
			  		margin-right: 3%;
			  		width:90vw;
			  		/*border:1px solid rgba(0,0,0,0.1);*/
			  		padding: 0 16px;
			  	}
		  	}
		}
	}
	
}
</style>