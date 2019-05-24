<template>
  <div id="app">
    <div id="left-panel" style="float: left;">
      <center>
        <div class="dragShovel" v-for="(shovel, index) in shovels" :key="index">
          <img
            id="shovel"
            src="./assets/schaufel.png"
            v-on:drag="handleMove"
            v-on:drop="endHandler"
            v-touch:moved="handleMove"
            v-touch:moving="handleMoving"
            v-touch:end="endHandler"
            v-if="shovel"
          >
        </div>
        <br>
        <br>
        <img id="controller-button" src="./assets/play.png">
        <img id="controller-button" src="./assets/stop.png" style="margin-left: 10%">
        <br>
        <br>
        <br>
      </center>
    </div>

    <div id="crocoWater">
      <img src="./assets/croco_wasser.png">
    </div>
    <div id="playground" v-on:drop="drop">
      <!-- ondrop="drop(event)" ondragover="allowDrop(event) -->
      <table>
        <tr v-for="(row, index) in playground" :key="index">
          <th v-for="(type, index) in row" :key="index">
            <img src="./assets/croco.png" v-if="type==0">
            <img src="./assets/schmutz.png" v-if="type==1">
            <img src="./assets/fels.png" v-if="type==2">
            <div class="empty" v-if="type==4"/>
          </th>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
// TODO: Auslagern in eigene Datei, damit auch im Template die Konstanten verwendet werden können
const CROCO = 0;
const STONE1 = 1;
const STONE2 = 2;
const GOAL = 3;
const EMPTY = 4;

export default {
  name: "app",
  data() {
    return {
      shovels: [true, true, true],
      playground: [
        [STONE1, EMPTY, STONE2, STONE1, GOAL],
        [STONE1, STONE2, STONE1, EMPTY, STONE2],
        [EMPTY, STONE1, STONE2, EMPTY, EMPTY],
        [EMPTY, STONE1, STONE2, STONE1, STONE1],
        [CROCO, STONE1, EMPTY, STONE2, STONE2]
      ]
    };
  },
  methods: {
    handleMove: function(ev) {
      console.log("handle drag");
    },
    handleMoving: function(ev) {
      console.log("handleMoving --> redraw");
    },
    endHandler: function(ev) {
      console.log("handle drop");
    },
    drag: function(ev) {
      ev.dataTransfer.setData("text", ev.target.id);
    },
    allowDrop: function(ev) {
      ev.preventDefault();
      return true;
    },
    drop: function(ev) {
      alert("sdad");
      ev.preventDefault();
      var dragged = ev.target;
      if (ev.target.id == "playground") {
        dragged.parentNode.removeChild(dragged);
        ev.target.appendChild(dragged);
      }
    },
    test: function() {
      /*alert("test");*/
    }
  }
};

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
body {
  background-image: url(./assets/sumpf_hg.jpg);
  background-size: cover;
}

th,
td {
  border: 1px solid #716b61;
}

table {
  height: 100%;
  width: 100%;
}

.empty {
  height: 54px;
  width: 75px;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#left-panel {
  background-color: #736f6d;
  width: 25%;
  position: relative;
  height: 100%;
  padding: 1%;
  border: 2px solid #666260;
  /*	box-shadow: 5px 5px rgba(0,0,0,0.5); */
}

#crocoWater {
  float: right;
  margin-right: 5%;
  margin-top: -50px;
  height: 120px;
}

#playground {
  background-color: #c7c3b9;
  width: 50%;
  position: relative;
  height: 390px;
  border: 2px solid #716b61;
  float: left;
  margin-left: 12%;
}

#controller-button {
  border: 2px solid transparent;
  &:hover {
    border: 2px solid #666260;
  }
}

.dragShovel {
  border: 2px solid transparent;
  width: 75px;
  height: 75px;
  padding: 1em;

  &:hover {
    border: 2px solid #666260;
  }
}
</style>
