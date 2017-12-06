<template>
  <canvas width="20" height="20" class="child" @click="clicked"></canvas>
</template>
<script>
export default {
  methods: {
    clicked () {
      this.$emit('newLeaf', this.value, this.height)
    }
  },
  mounted () {
    var children = document.getElementsByClassName('child')
    for (var i = 0; i < children.length; i++) {
      var child = children[i]
      var childCtx = child.getContext('2d')
      childCtx.fillStyle = 'rgb(46, 138, 227)'
      childCtx.clearRect(0, 0, 20, 20)
      childCtx.fillRect(0, 0, 20, 20)
      childCtx.moveTo(3, 10)
      childCtx.lineTo(17, 10)
      childCtx.moveTo(10, 3)
      childCtx.lineTo(10, 17)
      childCtx.lineWidth = 1
      childCtx.strokeStyle = 'white'
      childCtx.stroke()
    }
  },
  props: {
    value: {
      type: Number,
      required: false,
      default: 0
    },
    height: {
      type: Number,
      required: false,
      default: 0
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
canvas {
  margin: 0 auto;
  display: block;
}
</style>
