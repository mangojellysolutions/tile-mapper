<template>
  <div class="Mid">
    <div id="mapDiv">
      <canvas id="canvas" width="800" height="600"></canvas>
    </div>
    <div id="mapCSVDiv">
      <textarea style="width: 800px; height: 100px;" id="mapCSV"></textarea>
    </div>
  </div>
</template>
<script>
  const tileWidth = 64;
  const tileHeight = 64;
  let tilesAcross = 0;
  let tilesDown = 0;
export default {
  
  name: "Mid",
  data: function(){
    return {
    canvasMain: null,
    ctxMain: null
    }
  },
  mounted() {
    this.canvasMain =  document.getElementById("canvas");
    this.ctxMain = this.canvasMain.getContext("2d");
    this.$root.$on('new', () => this.new());
  },
  methods: {
    getImgUrl(image) {
      const images = require.context("../assets/image/", false, /\.png$/);
      return images("./" + image + ".png");
    },
    eraser: function(){
      this.ctxMain.fillStyle = "RED";
      this.ctxMain.fillRect(0,0,100,100);

    },
    new: function(){
      const img = new Image();
      
      img.src = this.getImgUrl('g4506');
      console.log(img.src )
      img.onload = () => {
        console.log( img.width)
        this.canvasMain.width = img.width;
        this.canvasMain.height = img.height;
        tilesAcross = Math.floor(img.width/tileWidth);
        console.log('tiles across', tilesAcross)
        tilesDown = Math.floor(img.height/tileHeight);
        console.log('tiles across', tilesDown)
        this.ctxMain.drawImage(img, 0, 0, img.width, img.height);
       // setTimeout(getTiles, 1000);
      };

    }
  }
}; //
//this.loadFullImage();
</script>
<style lang="css" scoped>
.Mid {
  grid-area: Mid;
}
#mapDiv{
  width:100%; 
  height:600px; 
  overflow: scroll;
}
</style>