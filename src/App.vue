<script setup type="module" lang="ts">
import Pixels from './components/Pixels.vue';
import { onMounted, ref } from 'vue';
  let width:number = 10;
  let height:number = 10;

  const TemplateArea = {width: width, height: height}
  let pixels: any = ref([]);

  let sizePixel = ref(30);
  let color: string = 'black';

  const changeWidth = ref('0')
  const changeHeight = ref('0')

  onMounted(() => {
    createSample()
  })

  function createSample(){
    console.log('1')
    let colorPixel = false;
    let count = 0

    for(let i = 0; i <= Math.round(width * height - 1); i++){
      if(width * height % 2 === 0 && count === width){
        count = 0
      }else{
        colorPixel = !colorPixel
      }

      pixels.value.push({color: colorPixel ? "#d6d6d6" : "#b5b5b5"});
      count++
    }

    TemplateArea.width = sizePixel.value * width
    TemplateArea.height = sizePixel.value * height
  }

  function changeColorPixel(index: number){
    if(color !== null) {
      const pixel = pixels.value[index];
      pixel.color = color;
    }
  }

  function chooseColor(event: any){
    color = event.target.value
  }

  function clear(){
    pixels.value = []
    createSample()
  }

  function zoom(event: number){
    if(event === -1){
      sizePixel.value -= 15

      if(sizePixel.value === 0) sizePixel.value = 1
      
    }else{
      sizePixel.value += 15
    }
    
    TemplateArea.width = sizePixel.value * width
    TemplateArea.height = sizePixel.value * height
  }

</script>

<template>
  <div class="main" >
    <div class="block-art">
      <div class="art" :style="{
        width: TemplateArea.width + 'px',
        height: TemplateArea.height + 'px',
      }">
  
        <Pixels 
        v-for="(el, index) in pixels" 
         :key="index" 
         :color="el.color" 
         :index="index"
         :sizePixel="sizePixel"
         :changeColorPixel
        />
      </div>
    </div>

    <div class="block-edit">
      <div class="colors-block">
        <input id="color" type="color" @change="chooseColor"/>
      </div>
      <div class="TemplateEdit">
        <button id="clear" @click="clear">Очистить</button>

        <div class="zoom">
          <button @click="zoom(-1)">-</button>
          <button @click="zoom(1)">+</button>
        </div>
      </div>
    </div>

  </div>
</template>

<style scoped lang="scss">
  .main{
    display: flex;

    justify-content: center;
    align-items: center;

    width: 100vw;
    height: 100vh;

    .block-art{  
      position: relative;
      right: 100px;
      .art{
        display: flex;
        flex-wrap: wrap;
        padding: 0;
        margin: 0;
      }
    }

    .block-edit{
      background-color: rgb(89, 88, 88);
      position: absolute;
      top: 0;
      right: 0;
  
      width: 250px;
      height: 100%;

      .colors-block{
        text-align: center;
        height: 200px;
    
        background-color: rgb(69, 69, 69);

        #color{
          position: relative;
          top: 20px;

          width: 150px;
          height: 150px;
      
          border-radius: 100%;
          border: 1px solid black
        }
      }


      .TemplateEdit{
        display: grid;
        margin: 5px;

        .zoom{
          padding: 5px;
          width: 100%;
          display: flex;
          justify-content: space-evenly;
          align-items: center;
          button{
            width: 100%;
            height: 100%;

            border: none;
            font-size: 20px;
          }
        }
      }
    }
  }
  #clear {
    width: 100px;
    height: 40px;

    padding: 10px;

    background-color: brown;
    color: white;
    border: none;
    border-radius: 5px;

    transition: all 0.1s;

    font-size: large;
  }
  #clear:hover{
    background-color: aliceblue;
    color: black
  }
</style>
