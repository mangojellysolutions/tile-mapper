<template>
  <div class="ToolBar">
    <div style="float:left">
      <!-- https://stackoverflow.com/questions/40491506/vue-js-dynamic-images-not-working-->
      <ul>
        <li v-for="(buttonGroup, bgIdx) in buttonGroups" v-bind:key="bgIdx">
          <a
            href="#"
            v-for="(buttonText, bgtIdx) in buttonGroup"
            v-bind:key="bgtIdx"
            :alt="buttonText"
            :title="buttonText"
            @click="callFunction(buttonText)"
          >
            <img :src="getImgUrl(buttonText)" :alt="buttonText" />
          </a>
          ||
        </li>
      </ul>
    </div>
    <div style="float:right">
      <a href="#" onclick="downloadIt()">
        <img src="../assets/icons/download.png" />
      </a>
      <a href="#" onclick="getTiles()">
        <img src="../assets/icons/build.png" />
      </a>
    </div>
  </div>
</template>
<script>
export default {
  /*
  the common pattern is as follows…

to affect a change in child, you update the props being passed

to affect change in parent, you $emit an event, that the parent then listens to

if you’re communicating outside of a child-parent relationship, you can bubble-up, and pass down data, or implement state management (usually with Vuex). Something like getUsers seems to be an ideal candidate for the type of async action that vuex could help handling

if you want to call an action using the passed props, you can use a watch for a data, and run function when the prop changes. (not the best pattern to use, but it can work)

if you don’t want to use vuex, or the watch pattern, using a bus may work for you too.
Great resource that’ll show you ow to implement: https://alligator.io/vuejs/global-event-bus/ 1.5k
*/
  name: "ToolBar",
  data: function() {
    return {
      buttonGroups: [
        ["new", "open", "save"],
        ["undo", "redo"],
        ["merge"],
        ["brush", "fill", "eraser"],
        ["select", "selectsame"],
        ["fliphorizontal", "flipvertical", "rotateleft", "rotateright"],
        ["grid"],
        ["download", "build"]
      ]
    };
  },
  methods: {
    getImgUrl(image) {
      const images = require.context("../assets/icons/", false, /\.png$/);
      console.log(images);
      return images("./" + image + ".png");
    },
    callFunction(functionName) {
      try {
        this[functionName](null);
      } catch (e) {
        console.log(functionName, 'function not found, emitting up');
        this.$root.$emit(functionName); 
        
      }
    },
    merge() {
      alert("merge");
       this.drawBox();
    },
  
  }
};
</script>
<style lang="css" scoped >
ul {
  list-style: none;
  display: inline;
  padding: 0px;
  margin: 0px;
}
li {
  display: inline-block;
}
a {
  vertical-align: middle;
}
img {
  vertical-align: middle;
  width: 3em;
  height: 3em;
}
.ToolBar {
  grid-area: ToolBar;
  font-size: 0.75em;
  border-bottom: solid 1px white;
  background-color: rgb(202, 202, 202);
  padding: 0.5em;
}
</style>