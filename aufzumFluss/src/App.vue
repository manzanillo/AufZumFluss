<template>
	<div id="app">
		<div id="left-panel" style="float: left;">
			<center>
			<div class="dragShovel"><img id="shovel1" src="./assets/schaufel.png" v-on:dragstart="drag" v-on:drag="test" v-on:drop="drop"/></div> <br />
			<div class="dragShovel"><img id="shovel2" src="./assets/schaufel.png" v-on:dragstart="drag"/></div> <br />
			<div class="dragShovel"><img id="shovel3" src="./assets/schaufel.png" v-on:dragstart="drag"/></div> <br /><br /><br />
			<img id="controller-button" src="./assets/play.png" /><img id="controller-button" src="./assets/stop.png" style="margin-left: 10%"/><br /><br /><br />
		</center></div>
		
		<div id="crocoWater"><img src="./assets/croco_wasser.png"/></div>
		<div id="playground" v-on:drop="drop" >
			<!-- ondrop="drop(event)" ondragover="allowDrop(event) -->
			<table>
				<tr><th><img src="./assets/schmutz.png"/></th><th><div class ="empty" /></th><th><img src="./assets/fels.png"/></th><th><img src="./assets/schmutz.png"/></th><th><div class ="empty" /></th></tr>
				<tr><th><img src="./assets/schmutz.png"/></th><th><img src="./assets/fels.png"/></th><th><img src="./assets/schmutz.png"/></th><th><div class ="empty" /></th><th><img src="./assets/fels.png"/></th></tr>
				<tr><th id="c_3"><div class ="empty" /></th><th><img src="./assets/schmutz.png"/></th><th><img src="./assets/fels.png"/></th><th><div class ="empty" /></th><th></th></tr>
				<tr><th id="c_2"><div class ="empty" /></th><th><img src="./assets/fels.png"/></th><th><img src="./assets/schmutz.png"/></th><th><img src="./assets/fels.png"/></th><th><img src="./assets/schmutz.png"/></th></tr>
				<tr><th id="c_1"><img id="croco" src="./assets/croco.png"/></th><th><img src="./assets/schmutz.png"/></th><th><div class ="empty" /></th><th><img src="./assets/fels.png"/></th><th><img src="./assets/fels.png"/></th></tr>
			</table>
		</div>
	</div>
</template>

<script>
export default {
	name: 'app',
	data: {},
	methods: {
		drag: function(ev){
			ev.dataTransfer.setData("text", ev.target.id);
		},
		allowDrop: function(ev){
			ev.preventDefault();
		},
		drop: function(ev){
			alert("sdad");
			ev.preventDefault();
			var dragged = ev.target;
			if (ev.target.id == "playground") {
				dragged.parentNode.removeChild(dragged);
				ev.target.appendChild(dragged);
			}
		},
		test: function(){
			/*alert("test");*/
		},
	}
}

/*function allowDrop(ev) {
  ev.preventDefault();
}

function drag(ev) {
	alert("dosth");
  ev.dataTransfer.setData("text", ev.target.id); 
}

function drop(ev) {
	ev.preventDefault();
	var contains = ev.dataTransfer.getData("text");
	ev.target.appendChild(document.getElementById(contains));
}*/

</script>

<style lang="scss">
body{
	background-image:url(./assets/sumpf_hg.jpg);
	background-size:cover;
}

th, td{
	border: 1px solid #716B61;
}

table{
	height: 100%;
	width: 100%;
}

.empty{
	height: 54px;
	width: 75px;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#left-panel
{
	background-color: #736F6D;
	width: 25%;
	position: relative;
	height: 100%;
	padding: 1%;
	border: 2px solid #666260;
/*	box-shadow: 5px 5px rgba(0,0,0,0.5); */
}

#crocoWater
{
	float: right;
	margin-right:5%;
	margin-top:-50px;
	height:120px;
}

#playground
{
	background-color: #C7C3B9;
	width: 50%;
	position: relative;
	height: 390px;
	border: 2px solid #716B61;
	float: left;
	margin-left:12%;
}

#controller-button
{
	border: 2px solid transparent;
	&:hover {
    border: 2px solid #666260;
  }
}

.dragShovel {  
	border: 2px solid transparent;
	width: 75px;
	height: 75px;

  &:hover {
    border: 2px solid #666260;
  }
}
</style>
