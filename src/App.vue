

<template>
  <div id="app">
  <!-- <div style="position:fixed;top:23px;z-index:2000">{{scrolled}}</div> -->
  	<div class="underline" :style="lineLeft"></div>
  	<header-nav></header-nav>
  	<main>
  		<slide1></slide1>
  		<slide2 :message="scrolled" :slide="sech"></slide2>
  		<slide3></slide3>
  		<slide4 :message="page"></slide4>
  	</main>
  	<footer-nav :message="page"></footer-nav>
  </div>
</template>

<script>
import HeaderNav from './components/header.vue'
import slide1 from './components/slide1.vue'
import slide2 from './components/slide2.vue'
import slide3 from './components/slide3.vue'
import slide4 from './components/slide4.vue'
import footerNav from './components/footer.vue'

import _ from 'lodash'


export default {
  name: 'app',
  components: {
    HeaderNav: HeaderNav,
    slide1: slide1,
    slide2: slide2,
    slide3: slide3,
    slide4: slide4,
    footerNav: footerNav

  },
  data () {
		return{
			scrolled: 0,
			lastScroll: 0,
			page:'',
			sech:'',
			sections:['#/Contact','#/About','#/Work/6','#/Work/5','#/Work/4','#/Work/3','#/Work/2','#/Work/1','#/Home'],
			relTagged:[],
			currKey:18,
			winHeight: window.innerHeight,
			slide1Height: 0,
			navPos:{
				Home:0,
				Work:0,
				About:0,
				Contact:0
			},
			lineLeft:{}
  	}
  },
  methods: {
  	handleScroll: function(){
        this.scrolled = document.body.scrollTop;
        this.setLocation()
        
    },
    underlineNav: function(pos){
    	
		this.lineLeft = {
			'left': pos[0]+'px',
			'width': pos[1]+'px'
		}
    },
	setLocation: function(){  //_.debounce(
		var rel = this.relTagged;

        for(var k = 0; k < rel.length; k++){
        	//console.log(this.scrolled, this.lastScroll)
        	if(this.scrolled >= rel[k] && this.currKey != k){
        		//console.log(this.scrolled, rel[k])
        		
	        	var currSection = this.sections[k]
	        	this.currKey = k
	        	//console.log(this.navPos[currSection.split('/')[1]], currSection.split('/')[1], currSection)
	        	this.sech = currSection
	        	this.underlineNav(this.navPos[currSection.split('/')[1]])

	        	this.page = currSection.split('/')[1]

	        	window.history.pushState(null, null, "/"+currSection+"");
	        	break;

	        	
	        	//console.log('get here')
	        }else if(this.scrolled >= rel[k] && this.currKey == k){
	        	break;
	        }
	        
        }

        this.lastScroll = this.scrolled
        //console.log('-------------------------')
	},  // 50),
    setSections: _.debounce(function(){
    	////Set the change positions for page
		var rels = document.querySelectorAll('[rel]');
		//var relList = []
		for (var key in rels) {
			if (rels[key].id != undefined ){
				var position = Math.round(document.body.scrollTop + rels[key].getBoundingClientRect().top) - 1 //1px fix
				if(position != this.relTagged[this.relTagged.length-1] && !isNaN(position)){
					this.relTagged.push(position) 
				}				
			}
		}
		this.relTagged = this.relTagged.reverse() 
		
		////set the nav positions
		var pages = document.querySelectorAll('a[href^="#"]');
		
		for(var p in pages){
			var navPosHTML = pages[p].innerHTML,
				rect = pages[p].getBoundingClientRect();

			this.navPos[navPosHTML] = [rect.left, rect.right - rect.left]

			if(p>2){
				break;
			}
		}

		////initially set underline
		var currLocation = window.location.hash.split('/')[1]
		this.lineLeft = {
			'left': this.navPos[currLocation][0]+'px',
			'width': this.navPos[currLocation][1]+'px'
		}

		///reset windowHeight
		this.winHeight = window.innerHeight
		this.slide1Height = document.getElementsByClassName('slide1')[0].clientHeight

    },300)
  },
  created: function() {
    window.addEventListener('scroll', this.handleScroll)
    window.addEventListener('resize', this.setSections)

  }, 
  mounted: function(){
  	this.setSections()
  	this.slide1Height = document.getElementsByClassName('slide1')[0].clientHeight
  	console.log(this.slide1Height)
  }
  	
}
</script>

<style lang="sass" >
@import 'stylesheets/partials/_normalize.scss';

@font-face {
    font-family: 'mont';
    src: url(src/fonts/Montserrat-Hairline.otf) format("opentype")
}
@font-face {
    font-family: 'orator';
    src: url(src/fonts/OratorStd.otf) format("opentype")
}
html,body{
  font-family:'orator';
  font-size:16px;
  width:100%;
  overflow-x: hidden;
   -webkit-overflow-scrolling:touch;
}
h1{
	font-size:5em;
	margin: 0px 0 10px;
	padding-top:86px;
}
p.tag{
	font-size:1.4em;
  	margin:0 auto;
  	max-width:50vw;
}
.container{
  position:relative;
  /*margin:0 auto;*/
  text-align:center;
  min-height:100vh;
  width:100%;
  z-index:3;
}
.row{
  position:relative;
  padding:0px 10vw;
  min-height:100vh;
  width:100%;
  box-shadow: 0 0 30px rgba(0,0,0,0.5)

}
* {
	box-sizing: border-box;
}
.underline{
	position:fixed;
	top:35px;
	left:9%;
	height:1px;
	width:6.5%;
	border-bottom:1px solid #ffc7b3;
	z-index: 101;
	transition:left 1s;
	box-shadow: 0px -1px 6px rgba(0,0,0,0.2);
}
@media only screen 
  and (min-device-width: 768px) 
  and (max-device-width: 1024px) 
  and (-webkit-min-device-pixel-ratio: 1) {
	  h1{
		font-size:4em;
		margin: 0px 0 10px;
		padding-top:86px;
	}
}
@media only screen 
  and (max-device-width: 767px){ 
	h1{
		font-size:2.5em;
		margin: 0px 0 10px;
		padding-top:86px;
	}
	p.tag{
		font-size:1em;
	  	margin:0 auto;
	  	max-width:90vw;
	}
	.row{
	  padding:0px 1vw;
	}

}
</style>
