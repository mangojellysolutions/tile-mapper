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
import Menu from './menu.vue'
import ToolBar from './ToolBar.vue'
import Left from './Left.vue'
import Mid from './Mid.vue'
import Right from './Right.vue'
import StatusBar from './StatusBar.vue'
export default {
  name: 'Container',
  components: {
    Menu,
    ToolBar,
    Left,
    Mid,
    Right,
    StatusBar
  },
  props: {
    msg: String
  }
}
</script>

<style lang="css" scoped>

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
