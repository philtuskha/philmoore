<template>
	<div class="container slide4" id="/Contact" rel="Contact">
		<div class="row">
			<h1>Contact</h1>
			<div class="contact-container" :class="{showmap: animate}">
				<div class="content">
					<a href="mailto:phil.tuskha@gmail.com" target="_blank">phil.tuskha@gmail.com<div class="guy"></div></a>
				</div>
				
				<div class="map"></div>
			</div>
		</div>
	</div>
</template>

<script>
export default{
	name:'slide4',
	props:['message'],
	data () {
		return{
			animate: false
		}
	},
	watch:{
	    message: function(){
	      this.animateMap()
	    }
	},
	methods:{
	    animateMap: function(){
	    	if(this.message == "Contact"){  // || this.message == "About"
	    		this.animate = true

	    	}else{
	    		this.animate = false
	    	}
	    }
	}
}
	

</script>

<style lang="sass">

@import '../stylesheets/partials/resources';

/*@-webkit-keyframes mymove {
    0%   {transform:translate(-150%, 0);}
    100%  {transform:translate(100%, 0);}
}*/

/* Standard syntax */
@keyframes mymove {
    /*0%   {transform:translate3d(-70%, 0, 0);}
    100%  {transform:translate3d(20%, 0, 20%);}*/
    /*0%   {left:-100%;}
    80%  {left:100%;}
    100%  {left:100%;}*/
    0%   {opacity:0;}
    50%  {opacity:0.2;}
    100%   {opacity:0.3;}
}


.slide4{
   z-index:3;
   background:#fff;

  .contact-container{
  	position:relative;

  	  .content{
  	  	position:absolute;
  	  	z-index:3;
  	  	width: 100%;
	  	height: 70vh;
	  	font-size:3em;
	  	padding-top:9vh;
	  	background:url(src/img/red_dot.svg) left top / 100% auto no-repeat;
	  	/*transform:translateX(0);*/
	  	
	  	a{
	  		position: relative;
	  		display:inline-block;
	  		text-decoration: none;
	  		color:$red;
	  		text-shadow: 1px 1px 1px rgba(255,255,255,1), -1px -1px 1px rgba(255,255,255,1) ;
	  		border-bottom:1px solid $red;
	  		transform:translateX(0);
	  		transition:transform 0.3s;
	  		padding:0;
	  		margin:0;

		  	.guy{
		  		position:absolute;
		  		top:-18px;
		  		left:0;
		  		height:77px;
		  		width:70px;
		  		background:url(src/img/worker.svg) left -10px / 92% 100% no-repeat;
		  		z-index:40;
		  		opacity:0;
		  		transform:translateX(0);
		  		transition:all 0.3s;
		  		border-bottom:1px solid $red;
		  		padding-bottom: 20px;
		  	}
		}
	  	a:hover{
	  		/*padding-left:70px;*/
	  		transform:translateX(30px);
	  	}
	  	a:hover .guy{
	  		opacity:1;
	  		transform:translateX(-70px);
	  	}	  	
  	  }
  
	  .map{
	  	position:absolute;
	  	width: 100%;
	  	height: 100vh;
	  	background:#e6e6e6;
	  	overflow:hidden; 
	  	position:relative;
	    -webkit-mask-image: url(src/img/dot_world.svg);
	    mask-image: url(src/img/dot_world.svg);
	    -webkit-mask-size: contain;
	    mask-size: contain;
	    -webkit-mask-repeat: no-repeat;
	    mask-repeat: no-repeat;
	    /*transform:translateX(0);*/
	    /*.meimg{
	    	opacity:0;
	    	transition:opacity 0.2s;
	    	
	    }*/
	    
		
	  }
	  .map::before{
	  	position:absolute;
	  	left:0%;
	  	top:-5%;
	  	transform:translateX(0);
	  	content:'';
	    width:100%;
	    height:100%;
	    background:url(src/img/me_bkg4.jpeg) center center / cover no-repeat;
		opacity:0.2;
		transition:all 0.5s;
	    /*@include three-gradient ($light-grey, 0%, $grey-blue, 40%, $light-grey, 100%)*/
	  }
	  
	  
	}
  h1{
  	color:$dark-grey;
  }

  img{
  	width:100vw;
  	margin-left:-11vw;
  }
  .showmap{
	  	/*.map::before{
	  		opacity:0.2;
	  		left:-20%;
	  		top:0;
		  	-webkit-animation: mymove 2s 1;
		    animation: mymove 2s 1;
		    transition:all 3s;
		  }*/
	  }
}
/* tablet */
@media screen and (min-width: 768px) 
and (max-device-width: 1024px){
	.slide4{
	  .contact-container{
		  	.content{
			  	padding-top:1vh;
			  	font-size:3em;
			  	/*border:1px solid grey;*/
			  	
			}
		}
	  
	}
}
/* phone */
@media screen 
  and (max-width: 767px){ 
  	.slide4{
  		h1{
  			font-size:4em;
  		}
	  .contact-container{
		  	.content{
			  	padding-top:20vh;
			  	font-size:1.5em;
			  	background:none;
			  	/*border:1px solid grey;*/
			  	a{
			  		border:none;
			  		.guy{
			  			opacity:1;
			  			width:100%;
			  			height:60px;
			  			border:none;
			  			background:url(src/img/worker.svg) left top / 100% 100% no-repeat;
			  			transform:translateX(0) translateY(3em)
			  		}
			  	}
			  	a::after{
				  content:'';
				  height:1px;
				  display:block;

				  @include three-gradient ($red-low, 0%, $red, 50%, $red-low, 100%);
				  
				}
			  	a:hover{
			  		/*padding-left:70px;*/
			  		transform:translateX(0px)
			  	}
			  	a:hover .guy{
			  		opacity:1;
			  		transform:translateX(0) translateY(3em)
			  	}
			  	/*a:active .guy{
			  		opacity:1;
			  		transform:translateX(158vw) translateY(3em)
			  	}*/			  	
			  	
			}
			.map{
			  	width:300%;
			  	opacity:0.5;
			}
		}

	  
	}
	
}


</style>