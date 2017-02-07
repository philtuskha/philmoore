<template>
	<div class="container slide1" id="Home">
		<div class="row">
	   		<h1>{{phil}}</h1>
	   		<p>{{tagline}}</p> 
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
							{class: '', item: ''}
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
  max-height:100vh;
  left:0;

  h1{ color: $dark-grey; }
  p{ 
  	/*text-align:justify;*/
  	color:$dark-grey;
  	font-size:1.4em;
  	margin:0 auto;
  	max-width:50vw;}
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
</style>