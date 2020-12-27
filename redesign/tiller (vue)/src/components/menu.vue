<template>
  <div class="Menu">File | Edit | View | Map | Help</div>
</template>

<script>
export default {
  name: "Menu"
};
</script>
<style lang='css' scoped>

.Menu {
     grid-area: Menu; 
     font-weight: bold;
        font-size: 12px;
        background-color: rgb(155, 155, 155);
        border-bottom: solid 1px rgb(116, 116, 116);
        padding: 5px 5px;
        }
</style>