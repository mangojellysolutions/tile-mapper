<template>
  <div class="grid-container">
    <Menu />
    <ToolBar/>
    <Left/>
    <Mid/>
    <Right/>
    <StatusBar/>
  </div> 
</template>
<script>
import Menu from './components/menu.vue'
import ToolBar from './components/ToolBar.vue'
import Left from './components/Left.vue'
import Mid from './components/Mid.vue'
import Right from './components/Right.vue'
import StatusBar from './components/StatusBar.vue'

export default {
  name: "App",
  components: {
    Menu,
    ToolBar,
    Left,
    Mid,
    Right,
    StatusBar
  }
};
</script>

<style>

body {
  font-family: Arial, Helvetica, sans-serif;
  margin: 0px;
  padding: 0px;
  height: 100%;
  width:100%;
  position: absolute;
}
.grid-container {
  height: 100%;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-rows: 0.1fr 0.1fr 3.7fr 0.1fr;
  gap: 1px 1px;
  background-color: #36393b;
  grid-template-areas: "Menu Menu Menu Menu" "ToolBar ToolBar ToolBar ToolBar" "Left Mid Mid Right" "StatusBar StatusBar StatusBar StatusBar";
}

</style>
