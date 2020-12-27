<template>
  <div class="Mid">
    <div id="mapDiv">
      <canvas id="canvasGrid" class="canvas" style="z-index: 2"></canvas>
      <canvas id="canvasMain" class="canvas" style="z-index: 1"></canvas>
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
//let showGrid = false;
let tiles = [];
let csv = []; 
export default {
  name: "Mid",
  data: function() {
    return {
      canvasMain: null,
      ctxMain: null
    };
  },

  mounted() {
    this.csvTextBox = document.getElementById("mapCSV");

    this.canvasMain = document.getElementById("canvasMain");
    this.ctxMain = this.canvasMain.getContext("2d");
    //this.ctxMain.fillStyle = "BLUE";
    //this.ctxMain.fillRect(0, 0,  this.canvasMain.width,  this.canvasMain.height);

    this.canvasGrid = document.getElementById("canvasGrid");
    this.ctxGrid = this.canvasGrid.getContext("2d");

    this.tileSheetCanvas = document.getElementById("tileSheetCanvas");
    this.tileSheetCtx = this.tileSheetCanvas.getContext("2d");
    this.clippingCanvas = document.createElement("canvas");
    this.clippingCanvas.width = tileWidth;
    this.clippingCanvas.height = tileHeight;
    this.clippingCtx = this.clippingCanvas.getContext("2d");
    this.$root.$on("new", () => this.new());
  },

  methods: {
    drawGrid: function() {
      let mapIdx = 0;
      this.canvasGrid.height = this.canvasMain.height;
      this.canvasGrid.width = this.canvasMain.width;
      //   this.ctxGrid.fillStyle = "rgb(0,0,0)";
      // this.ctxGrid.fillRect(0, 0,  this.canvasGrid.width,  this.canvasGrid.height);
      this.ctxGrid.fillStyle = "rgb(255,255,255)";
      this.ctxGrid.fillStyle = "rgba(0, 0, 200, 0.9)";
      this.ctxGrid.clearRect(
        0,
        0,
        this.canvasGrid.width,
        this.canvasGrid.height
      );

      this.ctxGrid.beginPath();
      console.log("jj");
      for (let y = 0; y < this.canvasGrid.height; y += tileHeight) {
        console.log(y);
        for (let x = 0; x < this.canvasGrid.width; x += tileWidth) {
          let tileIdx = csv[mapIdx];
          this.ctxGrid.fillText(tileIdx, x + 10, y + 10);
          this.ctxGrid.fillText(mapIdx, x + tileWidth / 2, y + tileHeight / 2);
          this.ctxGrid.rect(x, y, tileWidth, tileHeight);
          csv.push(tileIdx);
          mapIdx++;
        }
      }
      this.ctxGrid.stroke();
    },
    getImgUrl(image) {
      const images = require.context("../assets/image/", false, /\.png$/);
      return images("./" + image + ".png");
    },
    eraser: function() {
      this.ctxMain.fillStyle = "RED";
      this.ctxMain.fillRect(0, 0, 100, 100);
    },
    clipImageToTile: async function(x, y) {
      this.clippingCtx.drawImage(
        this.canvasMain,
        x,
        y,
        tileWidth,
        tileHeight,
        0,
        0,
        tileWidth,
        tileHeight
      );
      let newImage = await this.getImageDataUrl(this.clippingCanvas);
      let base64 = this.getBase64Image(newImage);
      let len = tiles.length;
      let match = false;
      let idx = 0;
      if (len > 0) {
        for (idx = 0; idx < len; idx++) {
          match = base64 == tiles[idx].base64;
          if (match) break;
        }
      }

      if (!match) {
        tiles.push({ image: newImage, base64: base64 });
        // tileDiv.appendChild(newImage);
        // document.getElementById('tileDiv').appendChild(newImage);
        return idx++;
      } else {
        return idx;
      }
    },
    getImageDataUrl: function(inCanvas) {
      return new Promise((resolve, reject) => {
        let newImage = document.createElement("img");
        newImage.onload = () => resolve(newImage);
        newImage.onerror = reject;
        newImage.src = inCanvas.toDataURL();
      });
    },
    getBase64Image: function(img) {
      // Create an empty canvas element
      let canvas = document.createElement("canvas");
      canvas.width = img.width;
      canvas.height = img.height;

      // Copy the image contents to the canvas
      let ctx = canvas.getContext("2d");
      ctx.drawImage(img, 0, 0);

      // Get the data-URL formatted image
      // Firefox supports PNG and JPEG. You could check img.src to
      // guess the original format, but be aware the using "image/jpg"
      // will re-encode the image.
      let dataURL = canvas.toDataURL("image/png");

      return dataURL.replace(/^data:image\/(png|jpg);base64,/, "");
    },
    getTiles: async function() {
      console.log("get tiles");
      //showGrid = false;
      //Check to see if we have anything in the csv, if so paint content first
      if (csv.length > 0) {
        //rebuildImage();
        csv = [];
        tiles = [];
      }

      //let idx = 0;
      for (let y = 0; y < this.canvasMain.height; y += tileHeight) {
        // let csvLine = "";
        for (let x = 0; x < this.canvasMain.width; x += tileWidth) {
          this.clippingCtx.clearRect(
            0,
            0,
            this.canvasMain.width,
            this.canvasMain.height
          );
          let tileIdx = await this.clipImageToTile(x, y);
          csv.push(tileIdx);
          //idx++;
        }
      }
      let csvLine = "";
      let i = 0;
      for (let y = 0; y < tilesDown; y++) {
        let csvText = null;
        for (let x = 0; x < tilesAcross; x++) {
          if (csvText == null) {
            csvText += csv[i];
          } else {
            csvText += "," + csv[i];
            if (tilesAcross - 1 == x) {
              console.log(x, "line break ----dance");
              csvText += "\n";
            }
          }
          i++;
        }
        csvLine += csvText;
      }
      this.csvTextBox.value = csvLine;

      //Build the tile sheets
      this.tileSheetCanvas.width = tileWidth * tiles.length;
      this.tileSheetCanvas.height = tileHeight;
      this.tileSheetCtx.clearRect(
        0,
        0,
        this.tileSheetCanvas.width,
        this.tileSheetCanvas.height
      );
      let x = 0;
      for (let tileImage of tiles) {
        this.tileSheetCtx.drawImage(tileImage.image, x, 0);
        x += tileWidth;
      }
      console.log("Complete tile update");
    },
    new: function() {
      const img = new Image();

      img.src = this.getImgUrl("g4506");
      console.log(img.src);
      img.onload = () => {
        console.log(img.width);
        this.canvasMain.width = img.width;
        this.canvasMain.height = img.height;

        tilesAcross = Math.floor(img.width / tileWidth);
        console.log("tiles across", tilesAcross);
        tilesDown = Math.floor(img.height / tileHeight);
        console.log("tiles across", tilesDown);
        this.ctxMain.drawImage(img, 0, 0, img.width, img.height);
        this.getTiles();
        console.log("draw grid");
        this.drawGrid();
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
#mapDiv {
  position: relative;
  width: 100%;
  height: 600px;
  overflow: scroll;
}
.canvas {
  position: absolute;
  top: 0;
  left: 0;
  width: 800;
  height: 600;
}
</style>