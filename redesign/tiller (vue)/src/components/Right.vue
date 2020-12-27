<template>
  <div class="Right">
    <div id="layerPane">
      <ul>
        <li>Layer 1</li>
        <li>Layer 2</li>
        <li>Layer 3</li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {};
</script>
<style lang="css" scoped>
ul {
  list-style : none;
  padding-left: 5em;
}
.Right {
  grid-area: Right;
  background-color: rgb(255, 255, 255);
  width: 100%;
}
</style>