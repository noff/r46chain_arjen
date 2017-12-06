<template>
  <div>
    <condition-component v-if="list[value] === 1">
      <div class="leftChild">
        <element-component :value='value * 2' :list="list" @newLeaf='newLeaf' :height="height + 1">
        </element-component>
      </div>
      <div class="rightChild">
        <element-component :value='value * 2 + 1' :list="list" @newLeaf='newLeaf' :height="height + 1">
        </element-component>
      </div>
    </condition-component>
    <action-component v-if="list[value] === 2">
      <element-component :value='value * 2' :list="list" @newLeaf='newLeaf' :height="height">
      </element-component>
    </action-component>
    <blank-component v-if="list[value] != 1 && list[value] != 2" :value='value' :height="height" @newLeaf='newLeaf'>
    </blank-component>
   </div>
</template>

<script>
import ConditionComponent from './ConditionComponent'
import ActionComponent from './ActionComponent'
import BlankComponent from './BlankComponent'
export default {
  name: 'element-component',
  components: {
    ConditionComponent,
    ActionComponent,
    BlankComponent
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
    },
    newLeafValue: {
      type: Number,
      required: false,
      default: -1
    },
    list: {
      type: Array,
      required: false,
      default: []
    }
  },
  methods: {
    newLeaf (value, height) {
      this.$emit('newLeaf', value, height)
    }
  },
  mounted () {
    var conditions = document.getElementsByClassName('condition')
    for (var i = 0; i < conditions.length; i++) {
      var c = conditions[i]
      var parent = c.parentNode
      var width = parent.offsetWidth
      c.setAttribute('width', width)
      var ctx = c.getContext('2d')
      ctx.fillStyle = 'rgb(46, 138, 227)'
      ctx.clearRect(0, 0, width, 80)

      var offset = width / 2 - 60
      ctx.moveTo(width / 2 - 75 + 145, 25)
      ctx.arcTo(width / 4 + offset + 50, 25, width / 4 + offset + 50, 50, 10)
      ctx.lineTo(width / 4 + offset + 50, 75)

      ctx.moveTo(width / 2 - 75 + 5, 25)
      ctx.arcTo(width / 4 + 5, 25, width / 4 + 5, 50, 10)
      ctx.lineTo(width / 4 + 5, 75)

      ctx.lineWidth = 3
      ctx.strokeStyle = 'gray'
      ctx.stroke()

      ctx.beginPath()
      ctx.moveTo(width / 4 + offset + 45, 65)
      ctx.lineTo(width / 4 + offset + 55, 65)
      ctx.lineTo(width / 4 + offset + 50, 75)
      ctx.closePath()
      ctx.fillStyle = 'gray'
      ctx.fill()

      ctx.beginPath()
      ctx.moveTo(width / 4 + 0, 65)
      ctx.lineTo(width / 4 + 10, 65)
      ctx.lineTo(width / 4 + 5, 75)
      ctx.closePath()
      ctx.fillStyle = 'gray'
      ctx.fill()

      ctx.beginPath()
      ctx.moveTo(width / 2 - 75 + 15, 0)
      ctx.lineTo(width / 2 - 75 + 135, 0)
      ctx.lineTo(width / 2 - 75 + 150, 25)
      ctx.lineTo(width / 2 - 75 + 135, 50)
      ctx.lineTo(width / 2 - 75 + 15, 50)
      ctx.lineTo(width / 2 - 75, 25)
      ctx.closePath()
      ctx.fillStyle = 'rgb(46, 138, 227)'
      ctx.fill()
      ctx.fillStyle = 'white'
      ctx.font = '20px Verdana'
      ctx.fillText('Condition', width / 2 - 75 + 30, 33)
    }
  }
}
</script>
