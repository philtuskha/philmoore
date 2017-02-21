<template>
	<header>
	   	<nav>
	   		<ul>
	   			<li v-for="n in nav"><a :href="'#/' + n.item">{{n.item}}</a></li>
	   		</ul>
	   	</nav>
   	</header>
</template>

<script>
export default{
	name: 'header-nav',
	props:['message'],
	data () {
		return{
			nav: [
				{item:'Home'},
				{item:'Work'},
				{item: 'About'}, 
				{item:'Contact'}
			],
			section: window.location.hash
		}
	},
	watch: {
		message: function(){
			
			this.followNav()
		}
	},
	methods:{
		 followNav: function(){

		// 	this.constants.lineLeft = {
		// 		'left': '500px'
		// 	}
		// 	console.log(this.constants.lineLeft)
		 }
	}
	// ,
	// mounted: function() {

	// 	window.onpopstate = function () {
 //              console.log(window.location.hash);
 //         }
	// }
}
</script>

<style lang="sass">

@import '../stylesheets/partials/_resources.scss';

header{
	position:fixed;
	top:0;
	left:0;
	width:100%;
	height:40px;
	z-index: 100;

	
	nav{
		position:relative;
		width:100%;
		height:40px;
		z-index: 100;

		ul{
			list-style: none;
			background:$red;
			border-bottom:1px solid #bc5959;
			height:40px;
			margin:0;
			padding:0;
			display: -webkit-flex;  /*do some css3 mixin stuff here*/
			-webkit-justify-content: space-around;
			display: flex;
			justify-content: space-around;
		}
		li{
			vertical-align: top;
			height:40px;
			padding:11px 20px;
			cursor:pointer;
		}

		a{
			height:40px;
			padding:8px 20px;
			font-family:'mont';
			letter-spacing: 0.2em;
			text-decoration:none;
			text-transform:uppercase;
			cursor:pointer;

		}
		@include linx(#fff, #fff, #ffc7b3, #ffc7b3)

		
	}
}
/* tablet */
@media screen and (min-width: 768px) 
and (max-device-width: 1024px){

	  
}
/* phone */
@media screen 
  and (max-width: 767px){ 
  	header{

  		nav{
  			ul{
  				/*display: -webkit-flex;  
				-webkit-justify-content: space-between;
				display: flex;
				justify-content: space-between;*/

  			}
  			li{
  				padding:12px 0px;
  			}
  			a{
  				font-size: 0.8em;
  				font-family:'mont-light';
  				letter-spacing: 0.1em
  			}
  		}
  	}
	
}
</style>