<template>
<div class="Left">
    <div class="propertiesPane">
        <table>
          <tr><td><strong>Property</strong></td><td><strong>Value</strong></td></tr>
          <tr v-for="(option, optionIdx) in options"
            v-bind:key="optionIdx"
          >
            <td>{{insertSpaces(optionIdx)}}</td><td><input :id="optionIdx" :value="option" type="text" /></td>
          </tr>
        </table>
        <div class="tileMergePane">
          <img id="primaryTileImg" src="../assets/icons/question-mark.png" /> <img src="../assets/icons/plus.png" /> <img id="secondaryTileImg" src="../assets/icons/question-mark.png" /> <br />
        </div>
      </div>
      <div class="tilePane">
      <strong>Tile Set</strong>
        <div id="tileDiv">
          <canvas id="tileSheetCanvas" width="50" height="800"></canvas>
        </div>
      </div>
  </div>
</template>
<script>
export default {
    name: 'Left',
    methods: {
      insertSpaces: function(string) {
        string = string.replace(/([a-z])([A-Z])/g, '$1 $2');
        string = string.replace(/([A-Z])([A-Z][a-z])/g, '$1 $2')
        string = string.charAt(0).toUpperCase() + string.slice(1);
        return string;
      }
    },
    data: function(){
    return {
        options:{
          orientation: "Orthogonal",
          tileWidth: 64,
          tileHeight: 64,
          mapWidth: 800,
          mapHeight: 600,          
          tilesAcross: 0,
          tilesDown:0,
          background:"RGB"
        }
    };
     }
    
}
</script>
<style lang="css" scoped>
a {
  vertical-align:middle;
}
img {
  vertical-align:middle;
  width:1.5em; 
  height:1.5em;
}
 input[type=text] {
        font-size: 1.5em;
        color: gray;
        width: 100%;
        border-style: none;
      }
.propertiesPane{
      background-color: rgb(255, 255, 255);
      height: 50%;
      overflow: auto;
    }
.Left { 
  background-color: rgb(118, 221, 34);
  position: relative;
  grid-area: Left; 
  height: 100%; 
  width:100%;
}
.propertiesPane > table {
    font-size: 1em;
    border-spacing: 0px;
}
.propertiesPane  td {
    padding: 5px;
    border-bottom: solid 1px rgb(204, 204, 204);
}
.tilePane {
   position: relative;
   background-color: rgb(255, 255, 255);
   height: 50%;
   width: 100%;
   overflow: auto;
}
.tileMergePane{
    background-color: rgb(255, 255, 255);
    padding: 1em;
}
#tileDiv {
  position: absolute;
  width:100%; 
  height: 100%; 
}
</style>