<template>
    <div class="progress-bar">
      <div v-for="(item, index) in data" :key="index" class="progress-item">
        <i v-if="item" class="uil uil-check"></i>
        <i v-else class="uil uil-capture"></i>
        <p>{{ String.fromCharCode(65 + index) }}</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      data: Array, // Pass your data array as a prop
    },
  };
  </script>

  
  