<template>
  <div id="app">
      <div class="container" >
       <div style="display: flex; justify-content: space-between;">

         <div style="margin-top: 100px">

            <div>
              <label for="images">Choose an image:</label>
              <select class="form-control" v-model="isSvg">
                  <option v-for="(shape, index) in shapes" :key="index">{{shape}}</option>
              </select>
            </div>
      
            <div >
              <label for="images">Choose radius:</label>
              <select style="width: 100%" class="form-control" v-model="radius" v-if="isDisabledCircle">
                  <option v-for="(c, index) in 100" :key="index">{{c}}</option>
              </select>
              <!-- <input style="width: 40%" class="form-control"  v-model="radius" :disabled="isDisabledCircle"  type="text" placeholder="radius"> -->
              <br>
              <label for="images"  v-if="isDisabledRectS">height: </label>
              <input style="width: 100%" class="form-control" type="text" v-model="height" v-if="isDisabledRectS" placeholder="height" />
                <br>
              <label for="images"  v-if="isDisabledRectS">width:</label>
              <input style="width: 100%" class="form-control" type="text" v-model="width" v-if="isDisabledRectS" placeholder="width"/>
              
              <label for="images">points:</label>
              <input style="width: 100%" class="form-control" type="text" v-model="points" v-if="isDisabledPolygon" placeholder="points looks like 220,10 300,210 170,250 123,234"/>
            </div>

            <div >
              <label for="images">Choose a color:</label>
              <select class="form-control" v-model="color">
                  <option v-for="(color, index) in colors" :key="index">{{color}}</option>
              </select>
            </div>
        
         </div>
       
       
         <div style="margin-top: 100px">

              <CircleSvg v-if="isCircle" :radius="radius" :color="color"/>

              <RectangleSvg v-if="isRectangle" :height="height" :width="width" :color="color"/>

              <SquareSvg v-if="isSquare" :height="height" :width="width" :color="color"/>

              <PolygonSvg v-if="isPolygon" :points="points" :color="color"/>

        </div>


       </div>  
      </div>
  </div>
</template>

<script>
//style="display: flex; justify-content: center; margin-top: 30px"
import CircleSvg from './components/CircleSvg'
import RectangleSvg from './components/RectangleSvg'
import SquareSvg from './components/SquareSvg'
import PolygonSvg from './components/PolygonSvg'

export default {
  name: 'App',
  
  components: {
    CircleSvg,
    RectangleSvg,
    SquareSvg,
    PolygonSvg
  },

  data() {
    return{
      isSvg: '',
      height: '',
      width: '',
      radius: '',
      points: '',
      disable: true,
      color: '',
      colors: [ "yellow", "blue", "green", "orange", "pink", "black", "purple" ],
      shapes: [ "circle", "rectangle", "square", "polygon"]
    }
  },

   mounted() {
    let local = JSON.parse(localStorage.getItem('svg'))
    
    this.isSvg =  local.isSvg
    this.height = local.height
    this.width =  local.width
    this.radius = local.radius
    this.color =  local.color
    this.points = local.points
  },

  updated() {
    if(this.isCircle || this.isRectangle || this.isSquare || this.isPolygon){
      this.createImage()
    }
  },

  computed: {

    isDisabledCircle() {
      return this.isSvg.length > 1 && this.isSvg === 'circle' //? this.disable === false : this.disable === true  
    },

    isDisabledRectS() {
      return this.isSvg.length > 1 && (this.isSvg === 'rectangle' || this.isSvg === 'square') //? this.disable === false : this.disable === true 
    },

    isDisabledPolygon() {
      return this.isSvg.length > 1 && this.isSvg === 'polygon'
    },

    isCircle() {
      return this.isSvg === 'circle' && this.radius.length > 0 && this.color.length > 0 
    },

    isRectangle() {
      return this.isSvg === 'rectangle' && this.height.length > 0 && this.width.length > 0 && this.color.length > 0 
    },

    isSquare() {
      return this.isSvg === 'square' && this.height.length > 0 && this.width.length > 0 && this.color.length > 0 
    },

    isPolygon() {
      return this.isSvg === 'polygon' && this.points.length > 0 && this.color.length > 0
    },
  },

  methods: {
    createImage() {
      let  payload = {
        isSvg: this.isSvg,
        radius: this.radius,
        height: this.height,
        width: this.width,
        color: this.color,
        points: this.points
      }
      localStorage.setItem('svg', JSON.stringify(payload));
    }
  }
}
</script>


