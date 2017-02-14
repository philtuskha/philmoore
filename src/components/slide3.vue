<template>
	<div class="container slide3" id="/About" rel="About">
		<div class="row">
		<h1>About</h1>
    <p class="tag">I am a self-taught programmer/designer who has been making things on the web for various clients and myself for over a decade. 
      I live somewhere in between the creative and technical aspects of the web.  </p>
		<div class="skills-content">
			<div class="bracket"></div>
			<ul>
				<li v-for="l in leftSide">
				<h3>{{l.title}}</h3>
				<p>{{l.content}}</p>
				</li>
			</ul>
			<ul>
				<li v-for="r in rightSide">
				<h3>{{r.title}}</h3>
				<p>{{r.content}}</p>
				</li>
			</ul>
		</div>
		</div>
	</div>
</template>

<script>
	export default{
	name:'slide3',
	data () {
		return{
			leftSide: [{
				title: 'Philosophy',
				content:'Make it Functional, Make it Beautiful, Make it Special, for all devices. Learn, Learn, Learn'
			},{
				title: 'For Hire',
				content: 'I have a lot of experience working for clients and with other talented people.  Contact me and let help you with your next project.'
			}],
			rightSide:[{
				title:'Languages',
				content:'HTML, CSS, Javascript, Python, PHP'
			},
			{
				title:'Frameworks, Libraries, Build Tools, etc.',
				content:'AngularJS, ViewJS, SASS, JQuery, Git, Github, Gulp'
			}]
		}
	}
}

</script>

<style lang="sass">
@import '../stylesheets/partials/resources';

.slide3{
  background:#5e5353;
  z-index:3;
  /*height:100vh;*/

  h1{
  	color:#fff;
  }
  p{
    color:#e3e8e8;
  }
  .skills-content{
  	width:80vw;
  	/*border:1px solid black;*/

  	

  	.bracket{
  		margin:0px;
  		width:100%;
  		height:100px;
  		background:url(src/img/icons/greyblue_bracket.svg) center bottom / 60% 60%  no-repeat;
  	}

  	ul{
  		margin:0;
  		padding:0;
  		display:inline-block;
  		vertical-align: top;
  		list-style: none;
  		width:48%;
  		height:60vh;
  		/*border:1px solid lightgreen;*/
  		

  		li{
  			display:block;
  			padding-bottom:10px;
  			/*border:1px solid pink;*/

  			h3{
  				margin:0.6em 0 1em 0;
  				color:#fff;
  				font-weight:bold;
  				font-size:1.5em;
  				letter-spacing: 0.3em;
  				justify-content: space-around;
  			}
  			p{
  				padding:0 2em;
  				color:$grey-blue;
  			}
  		}

  		li::after{
  			content:'';
  			width:50%;
  			height:40px;
  			border-right:1px solid $grey-blue;
  			display:block;
  		}
  	}
  }
}

</style>