<script setup lang="ts">

interface IPixelRops{
    color: string
    index: number
    resolution: number
    changeColorPixel: (index: number) => void
}
defineProps<IPixelRops>()

</script>

<template>
    <div 
      id="pixel" 

      :style="{
        backgroundColor: color, 
        width: resolution + 'px', 
        height: resolution + 'px'
      }" 

      @click="changeColorPixel(index)"
    ></div>
</template>

<style scoped>
    #pixel:hover{
        background-color: rgb(0, 136, 255);
    }
</style>