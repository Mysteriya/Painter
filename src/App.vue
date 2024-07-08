<script setup type="module" lang="ts">
import Pixels from './components/Pixels.vue';
import { onMounted, ref } from 'vue';

  let pixels: any = ref([]);

  const resolution: number = 50;
  const widthArea:number = 850;
  let color: string = 'black';

  onMounted(() => {
    createSample()
  })

  function createSample(){
    let colorPixel = false;

    for(let i = 0; i <= (widthArea * widthArea) / (resolution * resolution) - 1; i++){
      colorPixel = !colorPixel;
      pixels.value.push({color: colorPixel ? "#d6d6d6" : "#b5b5b5"});
    }
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

</script>

<template>
  <div class="main" >
    <div class="block-art">
      <div class="art" :style="{
        width: widthArea + 'px',
        height: widthArea + 'px',
      }">
  
        <Pixels 
        v-for="(el, index) in pixels" 
         :key="index" 
         :color="el.color" 
         :index="index"
         :resolution="resolution"
         :widthArea="widthArea"
         :changeColorPixel
        />
      </div>
    </div>

    <div class="block-edit">
      <div class="colors-block">
        <div>
          <input id="color" type="color" @change="chooseColor"/>
          <h3>цвет</h3>
        </div>
      </div>
  
      <button id="clear" @click="clear">Очистить</button>
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

        div {
          position: relative;
          top: 15px;

          h3 {
            color: white;
        
            font-size: 15px;
            font-weight: 300;
          }
          #color{
            width: 150px;
            height: 150px;
        
            border-radius: 100%;
            border: 1px solid black
          }
        }
      }
    }
  }
  #clear {
    width: 100px;
    height: 40px;

    background-color: brown;
    color: white;
    border: none;

    transition: all 0.1s;

    font-size: large;
  }
  #clear:hover{
    background-color: aliceblue;
    color: black
  }
</style>
