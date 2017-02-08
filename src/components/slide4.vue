<template>
	<div class="container slide4" id="Contact">
		<div class="row">
			<h1>Contact</h1>
			<div class="map">
				
			</div>
			
		</div>
	</div>
</template>

<script>
	

</script>

<style lang="sass">

@import '../stylesheets/partials/resources';

/*@-webkit-keyframes mymove {
    0%   {transform:translate(-150%, 0);}
    100%  {transform:translate(100%, 0);}
}*/

/* Standard syntax */
@keyframes mymove {
    /*0%   {transform:translate(-150%, 0);}
    100%  {transform:translate(100%, 0);}*/
    0%   {left:-100%;}
    100%  {left:100%;}
}


.slide4{
  z-index:3;
  max-height:100vh;

  .row{
  	
  }
  .map{
  	width: 100%;
  	height: 80vh;
  	background:#e6e6e6;
  	overflow:hidden; 
  	position:relative;/*url(src/img/dot_world.svg)center 20vh / 80% 80% no-repeat;*/
  	/*@include gradient ($light-grey, 0%, #ccc, 90%)*/
  -webkit-mask-image: url(src/img/dot_world.svg);
    mask-image: url(src/img/dot_world.svg);
    -webkit-mask-size: contain;
    mask-size: contain;
    -webkit-mask-repeat: no-repeat;
    mask-repeat: no-repeat;
    /* Safari 4.0 - 8.0 */
	
  }
  .map::before{
  	position:absolute;
  	left:-100%;
  	/*transform:translate(-150%, 0);*/
  	content:'';
  	/*-webkit-animation: mymove 15s infinite;
    animation: mymove 15s infinite;*/
    width:100%;
    height:100%;
    @include three-gradient ($light-grey, 0%, $grey-blue, 40%, $light-grey, 100%)
  }
  .map::after{
  	content:'';
  	position:absolute;
  	top:27.9%;
  	left:20.1%;
  	width:0.4vw;
  	height:0.4vw;
  	background:$red;
  	border-radius: 50%

  }
  h1{
  	color:$dark-grey;
  }

  img{
  	width:100vw;
  	margin-left:-11vw;
  }
}


</style>