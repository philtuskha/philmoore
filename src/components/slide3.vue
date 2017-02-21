<template>
	<div class="container slide3" id="/About" rel="About">
		<div class="row">
		<h1>About</h1>
    <p class="tag">I am a developer / designer living in North Carolina who has been making stuff on the web for various clients and myself for over a decade.  
    I love working for talented people, along side of talented people and by myself.</p>
		<div class="skills-content">
			<div class="bracket"></div>
			<ul>
				<li v-for="l in leftSide">
				<h3>{{l.title}}</h3>
				<p v-html="l.content"></p>
				</li>
			</ul>
			<ul>
				<li v-for="r in rightSide">
				<h3>{{r.title}}</h3>
				<p v-html="r.content"></p>
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
				content:'Make it Functional, Make it Beautiful, Make it Special, for all devices. Learn, Learn, Learn.'
			},{
				title: 'For Hire',
				content: 'I have a lot of experience working for clients and with other talented creative teams.  <a href="#/Contact">Contact me</a> and let help you with your next project.'
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
  

  h1{
  	color:#fff;
  }
  p{
    color:#e3e8e8;
    a, a:visited{
      color:$grey-blue;
    }
    a:hover, active{
      color:$light-grey;
    }
  }
  .skills-content{
  	width:100%;
  	/*border:1px solid black;*/

  	

  	.bracket{
  		margin:0px;
  		width:100%;
  		height:100px;
  		background:url(src/img/icons/greyblue_bracket.svg) center bottom / 50% auto  no-repeat;
  	}

  	ul{
  		margin:0;
  		padding:0;
  		display:inline-block;
  		vertical-align: top;
  		list-style: none;
  		width:48%;
  		height:60vh;
  		

  		li{
  			display:block;
  			padding-bottom:10px;

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

  		li:nth-child(1)::after{
  			content:'';
  			width:50%;
  			height:40px;
  			border-right:1px solid $grey-blue;
  			display:block;
  		}
  	}
  }
}
/* tablet */
@media screen and (min-width: 768px) 
and (max-width: 1024px){

    
}
/* phone */
@media screen 
  and (max-width: 767px){ 
    .slide3{
      h1{
        font-size:4em;
      }
      .bracket{
        display:none;
      }
      .skills-content{
        width:100%;
        margin-top:4em;
        ul{
          display:block;
          width:100%;
          height:auto;

          li:nth-child(2)::after{
            content:'';
            width:50%;
            height:40px;
            border-right:1px solid $grey-blue;
            display:block;
          }
        }
        ul:nth-child(3) li:nth-child(2)::after{
          padding:4em 0;
        }

       /* ul:nth-child(3) li:nth-child(2):after{
            padding-bottom:12em;
          }*/
      }
    }


  
}

</style>