<template>
  <div class="element">
    <canvas width="200" height="80" class="condition"></canvas>
    <slot/>
  </div>
</template>

<script>
export default {
  name: 'ConditionComponent'
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.element {
  position: relative;
}
.condition {
  margin-bottom: -15px;
  margin-top: 10px;
}
canvas {
  margin: 0 auto;
  display: block;
}
.leftChild {
  position: absolute;
  width: 50%;
  left: 5px;
}
.rightChild {
  position: absolute;
  width: 50%;
  right: 10px;
}
</style>
