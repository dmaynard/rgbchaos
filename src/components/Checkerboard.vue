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
  for (let i = 0; i < data.length; i += 4) {
    data[i] = Math.floor(Math.random() * 256);     // Red
    data[i + 1] = Math.floor(Math.random() * 256); // Green
    data[i + 2] = Math.floor(Math.random() * 256); // Blue
    data[i + 3] = 255;                             // Alpha (fully opaque)
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