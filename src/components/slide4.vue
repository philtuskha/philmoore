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

  .contact-container{
  	position:relative;

  	  .content{
  	  	position:absolute;
  	  	z-index:3;
  	  	width: 100%;
	  	height: 70vh;
	  	font-size:3em;
	  	padding-top:12vh;
	  	background:url(src/img/red_dot.svg) left top / contain no-repeat;
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

	  	}

	  	a:hover{
	  		/*padding-left:70px;*/
	  		transform:translateX(30px)
	  	}
	  	a:hover .guy{
	  		opacity:1;
	  		transform:translateX(-70px) rotate(0deg)
	  	}	  	
  	  }
  
	  .map{
	  	position:absolute;
	  	width: 100%;
	  	height: 70vh;
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
	  	left:-20%;
	  	top:-5%;
	  	transform:translateX(0);
	  	content:'';
	    width:100%;
	    height:100%;
	    background:url(src/img/me_bkg4.jpeg) center center / contain no-repeat;
		opacity:0.2;
		transition:all 0.5s;
	    /*@include three-gradient ($light-grey, 0%, $grey-blue, 40%, $light-grey, 100%)*/
	  }
	  
	  .guy{
  		position:absolute;
  		top:-18px;
  		left:0;
  		height:77px;
  		width:70px;
  		background:url(src/img/worker.svg) left top / 60px 60px no-repeat;
  		z-index:40;
  		opacity:0;
  		transform:translateX(0);
  		transition:all 0.3s;
  		border-bottom:1px solid $red;
  		padding-bottom: 20px;
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


</style>