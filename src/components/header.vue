<template>
	<header>
	   	<nav>
	   		<ul>
	   			<li v-for="n in nav"><a :href="'#' + n.item">{{n.item}}</a></li>
	   		</ul>
	   	</nav>
   	</header>
</template>

<script>
export default{
	name: 'header-nav',
	data () {
		return{
			nav: [
				{item:'Home'},
				{item:'Work'},
				{item: 'Skills'}, 
				{item:'Contact'}
			]
		}
	}
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
		width:100%;
		height:40px;
		z-index: 100;
	}
	nav{
		ul{
			list-style: none;
			background:$red;
			border-bottom:1px solid $rust;
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
		}

		a{
			height:40px;
			padding:8px 20px;
			font-family:$header-font;
			text-decoration:none;
			text-transform:uppercase;

		}
		@include linx(#fff, #fff, #ffc7b3, #ffc7b3)
	}
}
</style>