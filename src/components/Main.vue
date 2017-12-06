<template>
  <div id="container" v-bind:style="{ width: width + 'px' }">
    <element-component :value="1" :list="list" @newLeaf="newLeaf" :height="0">
    </element-component>
    <modalbox :value="addingValue" :list="list" @change='change' v-show="addingValue != -1" id="modalBox">
    </modalbox>
    <div class="save">
      <button @click="saveClick" class="saveButton">Save</button>
    </div>
  </div>
</template>

<script>
import ElementComponent from './ElementComponent'
import Modalbox from './Modalbox'
export default {
  name: 'Main',
  components: {
    ElementComponent,
    Modalbox
  },
  methods: {
    change (temp, value) {
      if (value === 2) {
        this.height = this.height - 1
      }
      this.list = temp
      var width = Math.pow(2, this.height) * 400
      if (width > this.width) {
        this.width = width
      }
      this.addingValue = -1
    },
    newLeaf (value, height) {
      var modal = document.getElementById('modalBox')
      modal.style.left = window.scrollX + window.innerWidth / 2 - 200 + 'px'
      modal.style.top = window.scrollY + window.innerHeight / 10 * 4 + 'px'
      this.addingValue = value
      this.height = height
    },
    saveClick () {
      var jsonObj = {
        name: '',
        leftChild: {},
        rightChild: {}
      }
      for (var i = 1; i < this.list.length; i++) {
        if (this.list[i] !== 1 && this.list[i] !== 2) {
          continue
        }
        var startObj = jsonObj
        var index = i
        var temp = []
        while (index > 1) {
          temp.push(index % 2)
          index = Math.floor(index / 2)
        }
        while (temp.length) {
          index = temp.pop()
          if (index % 2 === 0) {
            startObj = startObj['leftChild']
          } else {
            startObj = startObj['rightChild']
          }
        }
        if (this.list[i] === 1) {
          startObj['name'] = 'Condition'
        } else if (this.list[i] === 2) {
          startObj['name'] = 'Action'
        }
        startObj['leftChild'] = {}
        startObj['rightChild'] = {}
      }
      console.log(startObj)
    }
  },
  data () {
    return {
      list: [0, 0],
      addingValue: -1,
      width: 0,
      height: 0
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#container {
  min-width: 100%;
}
#modalBox {
  position: absolute;
  width: 400px;
  box-shadow: 0px 0px 1rem 0.2rem #ccc;
  padding: 1rem;
  background: white;
}
.save {
  position: absolute;
  top: 2rem;
  left: 2rem;
}
.saveButton {
  display: inline-block;
  margin-bottom: 0;
  font-weight: normal;
  text-align: center;
  vertical-align: middle;
  touch-action: manipulation;
  cursor: pointer;
  border: 1px solid transparent;
  white-space: nowrap;
  border-radius: 0.3rem;
  user-select: none;
  color: #fff;
  background-color: #337ab7;
  border-color: #2e6da4;
  margin: 1rem;
  padding: 0.5rem 2rem;
  font-size: 20px;
}
</style>
