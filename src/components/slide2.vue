<template>

	<div class="container slide2" id="/Work" rel="Work">
	<!-- <div id="counter">{{constants.dis}}</div> -->
		<div class="row">
			<div class="description">
				<section v-for="(desc, index) in description" :id=" '/Work/'+ index" :rel=" 'Work'+ index">
					<h1>{{desc.title}}</h1>
					<p class="tag">{{desc.tag}}</p>
					<div  class="rotate-details" :class="{ showRotateDeets: !carousel[indexCheck(slideAdjusted)].cover, showProject:readProject }"> <!-- > -->
						<div v-on:click="readProj">Project Goal</div>
						<div v-on:click="readImp">Implementation</div>
					</div>
					<!-- <p class="description" :class="{ hideP: !carousel[indexCheck(index)].cover }">{{desc.details}}</p> :class="{ hideCover: !carousel[index].cover }" -->
				</section>
			</div>
			<div id="karousel-wrap" :style="stickyWrap">
				<div id="karousel" :style="rotateObject" >
					<figure v-for="(car, index) in carousel" v-on:click="car.show = !car.show">
							<transition name="fade">
								<!-- <img v-if="!car.show" :src="car.imgUrl"> -->
								<object v-if="car.show" :data="car.frameUrl"></object>
							</transition>
							<div class="frame-cover" v-if="!car.show" :class="{ hideCover: !car.cover }"></div>
					</figure>
				</div>
				
				<div class="site-details" ref="sd" :class="{rotateRight: readProject, rotateLeft: readImplementation }">
					<div class="left-carousel" :class="{ showCar: !carousel[indexCheck(slideAdjusted)].cover, showProject:readProject}">
						<ul id="proj" ref="mine">
							<li>
								<h3><span v-for="h in description[slideAdjusted].left.headline" v-html="h"></span></h3>
								<span v-html="description[slideAdjusted].left.item"></span>
								
							</li>
							
						</ul>
						<div class="close-more" v-on:click="readProj" :class="{showCloseMore: readProject }"></div>
						<div class="read-more"  v-on:click="readProj" :class="{hideReadMore: readProject }"> read more </div> <!-- v-if="overflow(description[slideAdjusted].left.item)" -->
					</div>
					<div class="right-carousel" :class="{ showCar: !carousel[indexCheck(slideAdjusted)].cover, showImplementation:readImplementation }">
						<ul id="imp">
							<li>
								<h3><span v-for="h in description[slideAdjusted].right.headline">{{h}}</span></h3>
								<span v-html="description[slideAdjusted].right.item"></span>
							</li>
							
						</ul>
						<div class="close-more" v-on:click="readProj"  :class="{showCloseMore: readImplementation }"></div>
						<div class="read-more" v-on:click="readImp" :class="{hideReadMore: readImplementation}"> read more </div>
						<div class="tool-wrap">
							<h4>Tools:</h4>
							<p class="tools" v-text="description[slideAdjusted].right.tools"></p>
						</div>
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
					item: '<p>Sylvan Esso needed to direct traffic to their website to showcase a new single, <i>Radio</i>, and b-side, <i>Kick Jump Twist</i>.</p>'+
							'<p>The Band was between album cycles, and they wanted to push their brand past that of their last album, to be more bold and enigmatic.</p>'+
							'<p>The goal was to maintain focus on the new media and steer fans to listen to and buy the 12” single while maintaining the necessary contact, social media and tour information.</p>'+
							'<p>Anticipating changes, the band wanted to strip the site of all content and begin to populate it with content that served their future branding goals.</p>'
				},
				right:{
					headline:'Implementation',
					item: '<p>I worked closely with the band and their team to aquire stills from the video and other assets to come up with the overall aesthetic.</p>'+
							'<p>I worked with third party content (Youtube, Bandsintown & Shopify), to make the site easy to maintain and to keep it consistently up to date.<p>',
					tools: 'HTML - CSS - Javascript - jQuery - Photoshop - Bandsintown - Shopify',
				}
				
			},{
				title: 'ditl.me',
				tag:'An annonymous, self-policing, group-texting, web-app',
				left:{
					headline:'Project Goal',
					item: '<p>The goal with Day in the Life was to make the internet nice again, one day at a time. The concept came as a response to the multiple posting apps such as Twitter and Facebook that focus on user profiles.  I wanted to create an environment where users would focus less on themselves and more on the topics of conversation that most interested them, while still maintaining congeniality.</p>'+
						'<p>Believing in the common good, I wanted to build an app with a voting system controlled by users that would restrict other (bad) users from posting mean stuff while maintaining complete anonymity, thereby fostering the creation of a more open forum for discussing whatever comes to mind.</p>'
				},
				right:{
					headline:'Implementation',
					item: '<p>I Used Django and Postgress for the backend and developed a model consisting of profiles, posts, responses & votes.  Each post lasts for a 24 hour period, and each response and vote associated with that post lasts the same lifecycle.  You can cast a vote (Like or Troll) on the post or response.  If a user’s post or response receives three troll votes by three different users, that user and their comment will become restricted for a 24hr period.  If that user comes back to post more mean and unhelpful comments, they will be restricted for a week.</p>'+
						'<p>I also developed a ranking system based on user activity/popularity (like votes) and a notification system tied to user comments and votes</p>',
					tools:'HTML - CSS - jQuery - Django - Illustrator - Git - Github'
				}
			},{
				title: 'Bar Virgile',
				tag:'A Bar in Downtown Durham, NC',
				left:{
					headline:'Project Goal',
					item: '<p>Bar Virgile is a beautiful and unique bar located in downtown Durham, NC, specilizing in craft cocktails and small delicious plates.</p>'+
                    '<p>The owners put a lot of care into the interior design of their space, and they wanted the look and feel of the website to mimic the warm, inviting atmosphere of the bar itself.</p>'+
                    '<p>One of the challenges with the project was keeping the consistently rotating menus up to date.  The owners needed a way to easily maintain the menus, and given the hurried nature of the restaurant business, I needed to make that process as painless as possible </p>'
				},
				right:{
					headline:'Implementation',
					item: '<p>The owners provided wonderful photography of the interior of the bar and I chose to base the look of the site around those images.  The filigree was added as a frame to offset the natural boxy tendencies of the web</p>'+
                        '<p>I used a javascript plugin called, \'jeditable,\' which allows for inline editing directly on the page and a simple php script to store the information to a text file.  This allowed the owners to maintain the menus and other content simply, without having to enter into an elaborate CMS that they would have to become familiar with.</p>',
                    tools:'HTML - CSS - jQuery - PHP - Photoshop'
				}
			},{
				title: 'Tuskha',
				tag:'A music player / download component',
				left:{
					headline:'Project Goal',
					item: '<p>I wanted to create a listening experience where the visitor could stream and download music without re-directing to a third party site.</p>'+
                    	'<p>The Soundcloud widget has limited styling and playing capabilities, due to its content being wrapped in an iframe, and web stores often require a redirect to make your final purchase.</p>'+
                    	'<p>  Because the music download option was pay-what-you-want by donation only, I did not need an elaborate checkout experience. But most importantly, I wanted to give the visitor no reason to leave the listening experience. I needed to visually combine the Soundcloud API and a Shopify donation widget to create a full listening / downloading environment.</p>'
				},
				right:{
					headline:'Implementation',
					item: '<p>I used Javascript to access the Soundcloud API.  I was able to take the JSON waveform data provided to draw my own scalable / custom styled waveform using a canvas element as well as using the simple play and stop functionality.</p>'+
						'<p>I wrapped the Shopify donation checkout in an iframe to allow for https content and for the visitor to stay within the listening experience while downloading the music.</p>',
					tools:'HTML - CSS - jQuery - Soundcloud API - Shopify'
				}
			},
			{
				title: 'Bowerbirds',
				tag:'A band from The North Carolia Piedmont',
				left:{
					headline:'Project Goal',
					item: '<p>To make a beautiful and fully functioning website, in less than 6 hours. </p>'+
                    '<p>The Bowerbirds website had not been updated since the release of our last album, in 2012 (I write music for this band).  It had been originally set up as a blog and informational website, but the content was out of date.  We needed to make an announcement about some upcoming music that we were releasing to benefit a wonderful cause, so we decided it was time to update our site. </p>'
				},
				right:{
					headline:'Implementation',
					item: '<p>Derrick Anderson, a local photographer, provided the main image of the site</p>'+
						'<p>This site uses absolutely no javascript.  Just HTML and CSS to provide all the necessary routing to our various social media platforms, webstore and management contact.</p>',
					tools:'HTML - CSS'
				}
			},
			{
				title: 'This Site',
				tag:'My own portfolio site',
				left:{
					headline:'Project Goal',
					item: '<p>I needed to make a web portfolio that would showcase my previous work, but also would give an explanation of what my strengths are as a web developer / designer.  The site needed to be geared towards potential employers and also the general public looking for web work in various capacities.</p>'+
						'<p>The site needed to be easy to maintain so that as I had more work to show, I could easily add those examples.</p>'
				},
				right:{
					headline:'Implementation',
					item: '<p>I worked with Vuejs and specifically the vue-cli to streamline the build process and make any additional content easy to add.</p>'+
							'<p>For the home page, I designed an infographic that represented my full capabilities as a developer / designer as well as where I would be most useful in a team environment.</p>'+
								'<p>I chose a color palette that I liked in and of itself, but that could also work as a backdrop for my work samples, given that the examples themselves are websites that can be loaded and manipulated directly on this site.</p>',
					tools:'HTML - CSS - Javascript - Vue.js - Illustrator - Git - Github - Gulp'
				}
			}],
			carousel:[{
				show:false,
				cover:true,
				imgUrl:"src/img/sites/SE_full.jpg",
				frameUrl:"src/sites/sylvanesso/"

			},{
				show:false,
				cover:true,
				imgUrl:"src/img/sites/ditl_full.jpg",
				frameUrl:"/"

			},{
				show:false,
				cover:true,
				imgUrl:"",
				frameUrl:"src/sites/bowerbirds/"

			},{
				show:false,
				cover:true,
				imgUrl:"",
				frameUrl:"src/sites/tuskha/"

			},{
				show:false,
				cover:true,
				imgUrl:"src/img/sites/BV_full.jpg",
				frameUrl:"src/sites/barvirgile/"

			},{
				show:false,
				cover:true,
				imgUrl:"src/img/sites/ditl_full.jpg",
				frameUrl:"src/sites/ditl/"

			}],
			constants:{
				direction: 0,
				// dis: ''
			},
			rotateObject:{
				'transform':'rotateX(0deg)'
			},
			stickyWrap:{},
			slideNumber: 0,
			slideAdjusted: 0,
			slideTop: 0,
			lastSwitch: 0,
			switchSlide: 0,
			showSlide: 0,
			readProject:false,
			readImplementation:false,
			// readProjectBig:false,
			// readImplementationBig:false,
			// projOverflow:this.overflow('proj',0.49),
			// impOverflow:this.overflow('imp',0.46),
		}
	},
	watch: {
		slide: function(){
			this.stickyCarosuel()
		},
		message: function(){
			if(this.slideNumber != 0){
				this.rotateCarousel()
				// console.log(this.slideNumber)
			}
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
			var splitSlide = this.slide.split('/')

			if(splitSlide[1] == 'Home'){

				this.rotateObject = {
					transition:'transform 1.5s',
					transform:'rotateX(0deg)'
				}

				this.stickyWrap = {
					position:'absolute'
				}
				this.coverReset(0)
				this.slideNumber = 0
				this.slideAdjusted = 0



			}else if(splitSlide[1] == 'Work' && splitSlide[2] != '6'){
				//console.log('whahuh??')
				this.stickyWrap = {
					position:'fixed'
					
				}				

				this.lastSwitch = 0
				this.slideTop = this.message
				this.slideNumber = splitSlide[2]
				this.switchSlide = Math.round(this.$parent._data.winHeight * 0.2) + this.message
				this.showSlide = Math.round(this.$parent._data.winHeight * 0.7)  + this.message

				///for when skipping ahead with arrow nav or menu nav
				if(Math.abs(this.constants.direction - this.message) > this.$parent._data.winHeight/4){

					this.slideAdjusted = this.slideNumber - 1
					this.readImplementation = false
					this.readProject = false
					if(this.carousel[this.indexCheck(splitSlide[2] - 1)].cover){
						this.coverReset(null)
						this.carousel[this.indexCheck(splitSlide[2] - 1)].cover = false
					}

					this.stickyWrap = {
						position:'fixed'
						
					}

					this.rotateObject = {
						transition:'transform 1.5s',
						transform:'rotateX('+ ((splitSlide[2] - 1) * 60) +'deg)'
					}
				}


			}else if(splitSlide[1] == 'Work' && splitSlide[2] == '6'){
				this.stickyWrap = {
					position:'fixed'
					
				}
				this.slideNumber = 5
			}
			else if(splitSlide[1] == 'About' || splitSlide[1] == 'Contact' && splitSlide[2] != '6'){ //splitSlide[2] != '6'
				this.rotateObject = {
					transition:'transform 1.5s',
					transform:'rotateX(300deg)'
				}
				this.slideNumber = 0
				//this.direction = this.$parent._data.relTagged[5]
			}
		},
		rotateCarousel: function () { //_.throttle( 
				
				if( this.constants.direction - this.message < 0){
					if(this.message > this.switchSlide){
						var rot = this.rotateObject.transform,
							rotNum = parseInt(rot.split('(')[1].split('d')[0]),
							newRot = Math.round(this.slideNumber * 60)
						
						//rotate once if 
						if(rotNum != newRot){
							this.rotateObject = {
								transition:'transform 1.5s',
								transform:'rotateX('+newRot+'deg)'
							}
							this.coverReset(null)
							this.readImplementation = false
							this.readProject = false
						}

						//uncover once
						if(this.message > this.showSlide){
							if(this.carousel[this.indexCheck(this.slideNumber)].cover){
								//console.log(this.carousel[this.indexCheck(this.slideNumber)].cover)
								this.coverReset(this.indexCheck(this.slideNumber))	
							}
							this.slideAdjusted = this.slideNumber
						}


					}else{
						//console.log('?????? revealed already')
					}
				}else{
					// console.log(this.message, this.switchSlide - this.$parent._data.winHeight)
					if(this.message < this.switchSlide - this.$parent._data.winHeight){
						var rot = this.rotateObject.transform,
							rotNum = parseInt(rot.split('(')[1].split('d')[0]),
							newRot = Math.round((this.slideNumber - 1) * 60)
							//console.log(rotNum, newRot)
						//rotate once
						if(rotNum != newRot){
							
							this.rotateObject = {
								transition:'transform 1.5s',
								transform:'rotateX('+Math.round(((this.slideNumber - 1) * 60))+'deg)'
							}
							this.coverReset(this.indexCheck(this.slideNumber) + 1)

							this.slideAdjusted = this.slideNumber - 1
							this.readImplementation = false
							this.readProject = false

						}			
					}else{
						
						if(this.message < this.showSlide - this.$parent._data.winHeight){
							//console.log('down here')
							//uncover once
							//console.log(this.carousel[this.indexCheck(this.slideNumber)].cover, this.carousel[this.indexCheck(this.slideNumber - 1)].cover)
							if(!this.carousel[this.indexCheck(this.slideNumber)].cover){
								// console.log(this.carousel[this.slideAdjusted].cover)
								this.coverReset(null)
							}							
						}
					}
				}
				//console.log(this.constants.direction - this.message)
				this.constants.direction = this.message
			}, // 56 ),
		readProj: function(){
			console.log(window.innerWidth)
			console.log(this.$refs.sd.clientWidth)
			var largeScreen = this.$refs.sd.clientWidth <= window.innerWidth
			
				


			var r = this.rotateObject.transform.split(')')[0] + ')'

			if(this.rotateObject.transform.includes('translateX')){
				//moves project text from the middle

				this.readProject = false
				this.readImplementation = false
				

				//moves carosuel back to the center
				this.rotateObject = {
				'transition':'transform 1s',
				'transform':r 
				}
			}else{

				//moves project text to the middle
				this.readProject = true
				this.readImplementation = false
				

				//moves carosuel to the right
				this.rotateObject = {
				'transition':'transform 1s',
				'transform':r +' translateX(120%)'//this.rotateObject.transform + 
				}
			}
				
			
			
		},
		readImp: function(){
			this.readImplementation = true
			this.readProject = false
			//console.log(this.rotateObject.transform.split(')')[0])
			var r = this.rotateObject.transform.split(')')[0] + ')'
			if(this.rotateObject.transform.includes('translateX')){
				//moves project text from the middle
				this.readProject = false
				this.readImplementation = false

				//moves carosuel back to the center
				this.rotateObject = {
				'transition':'transform 1s',
				'transform':r 
				}
			}else{

				//moves project text to the middle
				this.readProject = false
				this.readImplementation = true

				//moves carosuel to the right
				this.rotateObject = {
				'transition':'transform 1s',
				'transform':r +' translateX(-120%)'//this.rotateObject.transform + 
				}
			}
		},
		overflow: function(text){
			// if(this.$refs.mine != undefined){
			// 	//console.log(text.length, (this.$refs.mine.clientWidth * 2.2))
			
			// 	if(text.length > (this.$refs.mine.clientWidth * 2.2)){
			// 		return true
			// 	}else{
			// 		return false
			// 	}
			// }
		}
		
	},
	mounted: function(){
		///SUCH A HACK!!!! getting direct link to work projects 
		setTimeout(function(){
			window.scrollTo(0, document.body.scrollTop + 2)
		}, 200)
		
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
  	
  	
	
		.description{
			display:block;
			margin:0 0 0 0%;
			width:100%;
			text-align:center;
			/*line-height: 2em;*/
			opacity:1;
			visibility:visible;
			transition:opacity 0.7s, visibility 0.7s;

		    section{
			  position:relative;
			  z-index:3;
			  height:10vh;
			  margin-bottom:90vh;
			}

			.rotate-details{
		  		/*position:absolute;
		  		left:0;*/
		  		background:rgba(0,0,0,0.11);
		  		height:1.7em;
		  		width:100%;
		  		text-align:left;
		  		z-index:23;
		  		opacity:0;
		  		transition:opacity 0.5s;
		  		display:none;
		  		/*margin-left:-15%;*/
		  		border-radius: 2px;
		  		cursor:pointer;
		  		

		  		div{
		  			width:50%;
		  			
		  			display:inline-block;
		  			height:1.7em;
		  			/*border-radius: 0 12px 12px 0;*/
		  			color:#8b8a8a;/*#706e6e;*/
		  			text-align:center;
		  			padding:0.4em 0.7em;

		  		}

		  		div:nth-of-type(2){
		  			float:right;
		  			border-left:1px solid #706e6e;
		  			/*border-radius: 12px 0 0 12px ; */
		  			/*text-align:left;*/
		  		}

		  	}
		  	.showRotateDeets{
		  		opacity:1;
		  	}

		}
	}
	#karousel-wrap{
	  position:absolute;
	  top:30vh;
	  left:0;
	  width:100%;
	  height:100vh;
	  z-index:2;
	  -webkit-perspective:1000px; 
	  perspective: 1000px;
	  /*background:#333;*/


	  	.site-details{
	  		position:absolute;
	  		top:0vh;
	  		left:0;
	  		width:100%;
	  		text-align:left;
	  		z-index:-1;
	  		transform-style: preserve-3d;
	  		transition:transform 1s;
	  		/*z-index:13;*/
	  		/*border:1px solid cyan;*/

	  		>div{
	  			/*position:relatve;*/
	  			/*z-index:4;*/
	  			display:inline-block;
	  			opacity:0;
	  			transition:opacity 0.5s;
	  			color:#fff;
	  			padding:0;
	  			color:#bfd0d1;
	  			transition:opacity 0.5s, transform 1s, width 0.2s;
	  			
	  			

	  			ul{
	  				position:relative;
	  				list-style: none;
	  				padding:0;
	  				margin:1em 0;
	  				overflow: hidden;
	  				

	  				li{
	  					padding:0 1em;
	  					pointer-events: none;
	  					
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
	  						letter-spacing: 0.05em;
	  						word-spacing:.1em;
	  						line-height: 1.5em;
	  						text-align: left;
	  						font-size:0.9em;
	  						
	  					}
	  					
	  				}
	  			}
	  			ul#proj{
	  				max-height:46vh;
	  			}
	  			ul#imp{
	  				max-height:32vh;
	  			}
	  				
	  			
	  			.tool-wrap{
	  				padding:1em;

  					p.tools{
  						font-family: 'orator';
  						font-size:0.8em;
  					}
  				}

	  			.read-more{
	  				cursor:pointer;
	  				padding:1em;
	  				text-align:center;
	  				visibility:visible;
	  				opacity:1;
	  				transition: all 0.3s;
	  				height:50px;
	  			}
	  			.hideReadMore{
	  				height:0;
	  				padding:0;
	  				opacity:0;
	  				visibility:hidden;
	  			}
	  				  			
	  		}

		  	.left-carousel{
		  		position:relative;
		  		text-align:justify;
		  		margin-left: 3%;
		  		width:16%;
		  		/*border:1px solid rgba(0,0,0,0.1);*/
		  		box-shadow: 0px 0px 10px rgba(0,0,0,0.1);
		  		
		  	}
		  	.right-carousel{
		  		position:relative;
		  		text-align: justify;
		  		float:right;
		  		margin-right: 3%;
		  		width:16%;
		  		/*border:1px solid rgba(0,0,0,0.1);*/
		  		box-shadow: 0px 0px 10px rgba(0,0,0,0.1);
		  	}
		  	.close-more{
				position:absolute;
				top:-9px;
				right:-9px;
				width:20px;
				height:20px;
				border-radius: 50%;
				border:1px solid $grey-blue;
				cursor:pointer;
				background:rgba(74,74,74,0.4);
				opacity:0;
				visibility:hidden;
				transition:all 0.2s;
			}

			.close-more::after{
				content:'';
				position:absolute;
				width:12px;
				height:1px;
				top:8px;
				left:3px;
				background:$grey-blue;
				transform:rotate(45deg);
				
			}
			.close-more::before{
				content:'';
				position:absolute;
				width:12px;
				height:1px;
				top:8px;
				left:3px;
				background:$grey-blue;
				transform:rotate(-45deg);
				
			}
			.showCloseMore{
				opacity:0.7;
				visibility:visible;
			}
			.showCloseMore:hover{
				opacity:1;
			}
		  	.showProject{
		  		width:40vw;
		  	}
		  	.showImplementation{
		  		width:40vw;
		  	}
		  	.showCar{
		  		opacity:1;
		  	}

		}
		.rotateLeft{
			transform:translateX(-27vw);
		}

		.rotateRight{
			transform:translateX(26vw);
			
		}
		


		#karousel{
		  position: absolute;
		  width:40%;
		  height:40vh;
		  left:30%;
		  top:15.5vh;
		  transform-style: preserve-3d;
		  /*transform:rotateX(0deg) translateY(100vh);*/

			figure{
			  border:1px solid rgb(70,70,70);
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
			  background:url(src/img/sites/SE_full.jpg)  left top / cover  no-repeat;  
			}
			figure:nth-child(2){
			  transform:rotateX(60deg) translate3d(0,0,34.64vh);
			  background:url(src/img/sites/TS_main.jpg), url(src/img/sites/TS_under.jpg);
			  background-size: 100%, 100%;
			  background-position: left top, left top;
			  background-repeat: no-repeat, repeat-y; 
			}
			figure:nth-child(3){
			  transform:rotateX(120deg) translate3d(0,0,34.64vh);
			  background-color:#f1ebda;
			  background-image:url(src/img/sites/BBS_top.jpg), url(src/img/sites/BBS_bottom.jpg);
			  background-size: 100%, 100%;
			  background-position: left top, left bottom;
			  background-repeat: no-repeat, no-repeat; 
			}
			figure:nth-child(4){
			  transform:rotateX(180deg) translate3d(0,0,34.64vh);
			  background-color:#e6e6e6;
			  background-image:url(src/img/sites/TSKA_front.png), url(src/img/sites/TSKA_back.jpg);
			  background-size: 90%, 100%;
			  background-position: center 30%, 0px 0%;
			  background-repeat: no-repeat, no-repeat;
			}
			figure:nth-child(5){
			  transform:rotateX(240deg) translate3d(0,0,34.64vh);
			  background:url(src/img/sites/BV_logo.png), url(src/img/sites/BV_top.png), url(src/img/sites/BV_bottom.png), url(src/img/sites/BV_sides.png),url(src/img/sites/BV_back.jpg);
			  background-size: 30%, 100%, 100%, 100%, cover;
			  background-position: center 40%, left top, left bottom, left top, left top;
			  background-repeat:no-repeat, no-repeat, no-repeat, repeat-y, no-repeat; 
			}
			figure:nth-child(6){
			  transform:rotateX(300deg) translate3d(0,0,34.64vh); 
			  background:url(src/img/sites/DITL_top.jpg), url(src/img/sites/DITL_bottom.jpg), url(src/img/sites/DITL_back.jpg);
			  background-size: 100%, 32.8%, 100%;
			  background-position: left top, left bottom, left top;
			  background-repeat: no-repeat, no-repeat, repeat-y; 
			}

			object{
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
			  right:0;
			  width:220%;
			  height:100%;
			  background:rgba(70,70,70,1);
			  opacity:1;
			  visibility:visible;
			  transition:opacity 1.5s, visibility 1.5s;
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
@media screen and (min-width: 768px) 
and (max-width: 1024px){

	  
}
/* phone */
@media screen 
  and (max-width: 767px){ 
  	.slide2{
  		.row{
  			.description{
  				/*margin: 0 0 0 21vw;*/

  				h1{
  					margin-bottom:0.1em;
  				}
  				p{
  					margin-bottom:1em;
  				}
  				.rotate-details{
					display:block;
				}
  			}
  		}
	  	#karousel-wrap{

		  	#karousel{
				width:70%;
				height:40vh;
				left:15%;
			}
			
			.site-details{
		  		top:0;
		  		left:-100%;
		  		width:300%;

		  		>div{
			  		ul#proj{
		  				max-height:none;
		  			}
		  			ul#imp{
		  				max-height:none;
		  			}
		  			.read-more{
		  				display:none;
		  			}
			  	}
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
			  	
			  	
			  	.showProject{
		  			/*width:40vw;*/
			  	}
			  	.showImplementation{
			  		/*width:40vw;*/
			  	}
		  	}
		  	.rotateLeft{
				transform:translateX(-96vw);
			}

			.rotateRight{
				transform:translateX(96vw);
			}
		}
	}
	
}
</style>