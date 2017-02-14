<template>
	<div class="container slide1" id="/Home" rel="Home">
		<div class="row">
	   		<h1>{{phil}}</h1>
	   		<p class="tag">{{tagline}}</p> 
	   		<div class="graphic">
	   			<div class="graphic-title">{{graphicTitle}}</div>
	   			<div v-for="section in graphicSections" :class="[section.class]">
	   				<ul v-for="layer in section.loop" :class="[layer.class]"> 
	   					<li v-for="item in layer.loop" :class="[item.class]" v-html="item.item"></li>
	   				</ul>
	   			</div>
	   		</div>
	   	</div>
	</div> 
</template>

<script>
export default{
	name: 'slide1',
	data () {
		return{
			phil: 'I\'m Phil Moore',
			tagline: 'a Creative Front-End Developer focused on making Unique and Interactive experiences on the web.',
			graphicTitle: 'I can help you build a website',
			graphicSections: [{
				class: 'graphic-header',
				loop: [
					{
						class: 'graphic-role',
						loop:[
							{class: '',item: 'Backend'},
							{class: '', item: 'Frontend'},
							{class: '', item: 'Design'}
						]
					},
					{
						class: 'graphic-lines',
						loop:[
							{class: 'through-line',item: ''},
							{class: 'vert-line',item: ''},
							{class: 'vert-line', item: '<div>or Hire me to your team</div>'}
						]
					}
				]
			},
			{
				class: 'graphic-content',
				loop: [
					{
						class: 'backend',
						loop:[
							{class: '', item: 'Python, Django, PHP, Wordpress'},
							{class: '', item: ''},
							{class: '', item: 'SQL, Posgress, MYSQL'},
							{class: '', item: ''},
						]
					},
					{
						class: 'frontend',
						loop:[
							{class: '',item: ''},
							{class: '',item: ''},
							{class: '',item: 'HTML, CSS, SASS, Javascript, JQuery, Angular.js, View.js'},
							{class: '', item: 'or Hire me to your team'}
						]
					},
					{
						class: 'design',
						loop:[
							{class: '',item: 'Conceptualize, Create, Nitpick'},
							{class: '', item: ''},
							{class: '', item: 'Collect your magic Artifacts'},
							{class: '', item: ''},
						]
					},
				]
			}]
		}			
	}
	

}
</script>

<style lang="sass">
@import '../stylesheets/partials/_resources.scss';

.slide1{
  background:$light-grey;
  position:relative;
  left:0;

  h1{ color: $dark-grey; }
  p{ 
  	color:$dark-grey;
  	
  }
}

.graphic{
  margin:0;

	li, ul{
	  padding:0;
	  margin:0;
	}
	.graphic-title{
	  height:170px;
	  color:$red;
	  background:url(src/img/icons/graphic/red_bracket.svg) 50% bottom / 92% 92%  no-repeat;
	  font-size:1.1em;
	  margin-top:40px;
	}

	ul.graphic-role{
	  list-style:none;
	  margin-bottom: 1.2em;
	
		li{
		  vertical-align: top;
		  display:inline-block;
		  width:33.33%;
		  color:$dark-grey;
		  font-size:1.2em;
		}

		li:nth-child(1){
		  text-align:left;
		  padding-left:1%;
		}
		li:nth-child(2){
		  
		}
		li:nth-child(3){
		  text-align:right;
		  padding-right:1%;
		}
	}

	ul.graphic-lines{
	  list-style: none;
	  position:relative;
	  margin:0 4%;
	
		.through-line{
		  position:absolute;
		  top:30px;
		  list-style: none;
		  height:1px;
		  width:100%;
		  border-bottom:1px solid $grey-blue;
		}
		.vert-line{
		  border-left:1px solid $grey-blue;
		  display:inline-block;
		  vertical-align:top;
		  width:50%;
		  height:60px;
		}
		.vert-line:nth-of-type(1){
		  border-left:1px solid $grey-blue;
		  border-right:1px solid $grey-blue;
		}
		.vert-line:nth-of-type(3){
		  border-right:1px solid $grey-blue;
		}
		div{
		  position:relative;
		  z-index:1;
		  margin:10px 0 0 18%;
		  padding-left:2%;
		  height:40px;
		  text-align:left;
		  border-left:1px solid $red;
		  color:$red;
		  @include gradient ($light-grey, 4px, transparent, 0)
		}
		div::before{
		  content:'';
		  position:absolute;
		  left:-5px;
		  width:7px;
		  height:40px;
		  @include gradient ($light-grey, 4px, transparent, 0)
		}
	}
	.graphic-content{
		width:100%;
	
		ul{
		  display:inline-block;
		  width:33.33%;
		  list-style: none;
		  vertical-align:top;
		}
		ul li{
		  color: $grey-blue;
		}
		ul.backend{

			li{
			  text-align:left;
			}
			li:nth-child(odd){
			  border-left:1px solid $grey-blue;
			  margin-left:12%;
			  padding:4% 20% 5% 5%;
			}
			li:nth-child(even){
			  height:70px;
			}
			li:nth-child(2){
			  background:url(src/img/icons/graphic/server2.svg)  8% top / 12% 100%  no-repeat;
			}
			li:nth-child(4){
			  background:url(src/img/icons/graphic/database2.svg) 6.5% top / 12% 100%  no-repeat;
			}
		}
		ul.frontend{
			li:nth-child(1){
			  background:url(src/img/icons/graphic/screens.svg) left top / 100% 100%  no-repeat;
			  margin:10px 0 10px 0px;
			  height:120px;
			}
		}
		ul.design{
		  text-align:right;
		
			li:nth-child(odd){
			  border-right:1px solid $grey-blue;
			  padding:4% 5% 4% 20%;
			  margin: 0 12%;
			}
			li:nth-child(even){
			  height:70px;
			}
			li:nth-child(2){
			  background:url(src/img/icons/graphic/square.svg)  92% top / 14% 100%  no-repeat;
			}
			li:nth-child(4){
			  background:url(src/img/icons/graphic/jewel.svg) 94.5% top / 14% 100%  no-repeat;
			}
		}
	}
}
/* tablet */
@media only screen and (min-device-width: 768px) 
and (max-device-width: 1024px){

	  
}
/* phone */
@media only screen 
  and (max-device-width: 767px){ 

	.graphic{
		/*width:90vw;*/
		.graphic-title{
		  height:auto;
		  background: none;
		  border-bottom:1px solid $red;
		  width:80%;
		  margin:2em 0 5em 10%;
		}
		.graphic-header{
			display:none;
		}
		
		.graphic-content{
			width:100%;
			margin:0 auto;
		
			ul{
			  display:block;
			 width:100%;
			}
			ul li{
			  vertical-align: top;
			  display:inline-block;
			  padding:0;
			}
			
			ul.backend{
				position:relative;
				margin-bottom:13vh;
				li{
				  width:50%;

				}
				li:nth-child(odd){
				  margin-left:0%;
				  padding:4% 20% 5% 5%;
				}
				li:nth-child(even){
				  float:left;
				  margin:0;
				  height:90px;

				}
				li:nth-child(2){
				  background-size: 20%;
				  background-position: 86% center;
				}
				li:nth-child(4){
				  background-size: 20%;
				  background-position: 86% center;
				}
			}
			ul.backend::before{
				content:'Backend';
				position:absolute;
				top:-1.6em;
				left:25%;
				width:50%;
				font-size:2em;
				color:$dark-grey;
			}
			ul.backend::after{
				content:'';
				position:absolute;
				top:0%;
				left:50%;
				border-left:1px solid $grey-blue;
				width:1px;
				height: 200vh;
				z-index:-100;

			}
			ul.frontend{
				position:relative;
				margin:3em 0 0;
				text-align:center;
				clear:both;

				li{
					display:block;
					vertical-align: top;
					/*border:1px solid;*/
					width:100%;

				}
				li:nth-child(1){
				  background: $light-grey url(src/img/icons/graphic/screens.svg) left center / 80% 90%  no-repeat;
				  background-position: center center;
				  margin:0;
				  
				}
				li:nth-child(2){
					display:none;
				}
				li:nth-child(3){
				  padding:4% ;
				  background: $light-grey;
				  text-align:center;
				}
				li:nth-child(4){
				  color:$red;
				  border-bottom:1px solid $red;
				  background: $light-grey;
				  height:2em;
				  margin-top:0;
				  position:relative;
				  left:18%;
				  padding:0.5em 0 0;
				  text-align:center;
				  margin-top: 4em;
				  width:66%;
				}
				li:nth-child(4)::after{
				  content:'';
				  position:absolute;	
				  left:0;
				  top:2em;
				  background:$light-grey;
				  height:0.5em;
				  width:100%;
				}
			}
			ul.frontend::before{
				content:'Frontend';
				position:absolute;
				top:-1.6em;
				left:25%;
				font-size:2em;
				width:50%;
				color:$dark-grey;
				background: $light-grey;
				padding-top:0.4em;
			}
			ul.design{
			  text-align:left;
			  position:relative;
			  margin:16vh 0 0;
			  padding-bottom:10vh;

				li{
					display:inline-block;
					width:50%;
				}
				li:nth-child(odd){
				  margin:0;
				  padding:4% 20% 5% 5%;
				  border-right:none;
				  border-left:1px solid $grey-blue;
				  
				}
				li:nth-child(even){
				  float:left;
				  clear:left;
				  margin:0;
				}
				li:nth-child(2){
				  background-size: 20%;
				  background-position: 86% center;
				}
				li:nth-child(4){
				  background-size: 20%;
				  background-position: 86% center;
				}
			}
			ul.design::before{
				content:'Design';
				position:absolute;
				top:-1.6em;
				left:25%;
				width:50%;
				font-size:2em;
				color:$dark-grey;
				text-align:center;
				background:$light-grey;
				padding-top:0.4em;
			}
		}
	}
	
}
@media only screen and (min-device-width: 530px)
	and (max-device-width: 767px)
  {
  	.graphic{
  		.graphic-title{
		  width:60%;
		  margin:4vh 0 8vh 20%;
		}
  		.graphic-content{
  			ul.backend{
  				li:nth-child(2){
				  background-size: 10%;
				}
				li:nth-child(4){
				  background-size: 10%;
				}
			}
			ul.frontend{
				li:nth-child(4){
				  left:27.5%;
				  width:45%;
				}

			}
			ul.design{
  				li:nth-child(2){
				  background-size: 10%;
				}
				li:nth-child(4){
				  background-size: 10%;
				}
			}
		}
	}
  }

</style>