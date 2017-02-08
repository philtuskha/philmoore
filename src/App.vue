

<template>
  <div id="app">
  <div style="position:fixed;top:23px;z-index:2000">-->{{scrolled}}</div>
  	<header-nav></header-nav>
  	<main>
  		<slide1></slide1>
  		<slide2 :message="scrolled"></slide2>
  		<slide3></slide3>
  		<slide4></slide4>
  	</main>

  </div>
</template>

<script>
import HeaderNav from './components/header.vue'
import slide1 from './components/slide1.vue'
import slide2 from './components/slide2.vue'
import slide3 from './components/slide3.vue'
import slide4 from './components/slide4.vue'


export default {
  name: 'app',
  components: {
    HeaderNav: HeaderNav,
    slide1: slide1,
    slide2: slide2,
    slide3: slide3,
    slide4: slide4

  },
  data () {
		return{
			scrolled: 0 
  	}
  },
  methods: {
  	handleScroll: function(){
        this.scrolled = document.body.scrollTop;
    }
  },
  created: function() {
    window.addEventListener('scroll', this.handleScroll)
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
}
h1{
	font-size:5em;
	margin: 26px 0 10px;
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
  padding:60px 10vw;
  min-height:100vh;
  width:100%;
  box-shadow: 0 0 30px rgba(0,0,0,0.5)

}
* {
	box-sizing: border-box;
}
</style>
