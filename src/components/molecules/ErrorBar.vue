<template>
    <div class="error-bar">
      ERROR: {{ error_msg }}
    </div>
  </template>
  
  <script setup>

    defineProps({
      error_msg: {
        type: String,
        required: true,
      },
    });
  </script>
  
  <style scoped>
  .error-bar {
    position: fixed;
    bottom: 0;
    left: 0;
    width: 100%;
    background-color: red;
    color: white;
    text-align: center;
    padding: 10px;
    font-size: 16px;
    font-weight: bold;
    box-shadow: 0 -2px 5px rgba(0, 0, 0, 0.3);
  }
  </style>