<template>
  <canvas ref="canvas" :width="width" :height="height"></canvas>
</template>

<script setup>
import { ref, onMounted } from 'vue';
// import AttractorObj from '../modules/Attractor.js'; // Import DummyClass

const width = ref(window.innerWidth);
const height = ref(window.innerWidth); // Maintain square aspect ratio
const canvas = ref(null);

onMounted(() => {
  const ctx = canvas.value.getContext('2d');
  const imageData = ctx.createImageData(width.value, height.value);
  const data = imageData.data;
  // const ao = new AttractorObj(); // Create an instance of DummyClass
  // Generate random RGBA values for each pixel
  let w = width.value;
  let size = w/8;
  let base = 0;
  
  console.log( "width = ",  width.value);
  for (let j = 0; j < height.value; j++) {
    for (let i = 0; i < width.value; i++) {

        data[base++] = Math.floor(i/size)*255/8 ;     // Red
        data[base++] = Math.floor(j/size)*255/8 ; // Green
        data[base++] = Math.floor(i/size)*255/8 ; // Blue
        data[base++] = 255;                             // Alpha (fully opaque)
     }
}

  // Put the image data onto the canvas
  ctx.putImageData(imageData, 0, 0);
});
</script>

<style scoped>
canvas {
  display: block;
  margin: 10 auto;
}
</style>