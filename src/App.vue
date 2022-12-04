<template>
  <div
    id="box"
    @mousedown="mouseDown"
  >
  <MovingObject
    v-for="(item, index) in items"
    :key="index"
    :position="item[positionNumber]"
  />
</div>
</template>

<script>
import MovingObject from './components/MovingObject.vue'

let items = [] //массив, содержащий координаты положений для каждого элемента
let windowSize = [document.documentElement.clientWidth, document.documentElement.clientHeight] //размеры окна
let elW = Math.floor(windowSize[0]*0.05) //ширина элемента
let elH = Math.floor(windowSize[0]*0.05*1.4065) //высота элемента
let gap = Math.floor(elW / 96 ) //размер сдвига карт в колоде
if (gap == 0) gap = 1
let groupWidth = Math.floor((windowSize[0]-16)/5) //ширина экрана, выделенная под колоду
let groupWMargin =Math.floor( groupWidth - ( gap*2*49 + elW)/2) //горизонтальный отступ между колодами
let groupHeight= Math.floor((windowSize[1]-16)/2) //высота экрана, выделенная под колоду
let groupHMargin =Math.floor( (groupHeight - ( gap*49 + elH)/2)/2) //вернтикальный отступ между колодами
let lineWMargin = Math.floor((windowSize[0]- elW - 16)/49) //горизонтальный отступ разложенных карт
let lineHMargin = Math.floor((windowSize[1]- elH - 16)/9) //вертикальный отступ разложенных карт
let lineGap = Math.floor((windowSize[0] - (lineWMargin*49+elW+16))/2) //отступ для вертикального выравнивания всех разложенных карт

for(let i = 0; i<500; i++){
  let group = Math.floor(i/50)
  let line = Math.floor(i/250)
  items[i] = [[((i - 50*group) * gap*2 + group*groupWMargin + groupWMargin - 5*groupWMargin*line),(i - 50*group + line*groupHMargin*2 + groupHMargin)],[(i - 50*group)*lineWMargin + lineGap, group*lineHMargin]]
}

export default {
  name: 'App',
  components: {
    MovingObject,
  },
  data() {
    return {
      items: items,
      positionNumber: 0
    }
  },
  methods: {
    mouseDown() 
    {
    console.log(11)
    if(this.positionNumber == 1){
      this.positionNumber = 0
    }else{
      this.positionNumber = 1
    }
    },
  }
}
</script>

<style>
#box {
  width: 100vw;
  height: 100vh;
  background: linear-gradient(0deg, rgb(153 127 115) 0%, rgb(215 215 215) 100%);
  padding: 8px;
  box-sizing: border-box;
}
</style>
