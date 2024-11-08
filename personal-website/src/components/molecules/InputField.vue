<script setup>
  defineProps({
    type: {
      type: String,
      required: true
    },
    class: {
      type: String,
      required: true
    },
    dt: {
      required: false
    }
  })
  const model = defineModel()
</script>

<template>
  <input :type="type" :class="class" v-model="model">
</template>

<style>
  input{
    margin-left: 2vh;
    height: 5vh;
    font-size: 1.7vw;
    padding: 1.2vh;
    border: 2px solid #ddd;
    border-radius: 5px; 
    outline: none;
    box-sizing: border-box;
  }
  input.tournament-id {
    width: 7vw;
  }
  input[type="number"]::-webkit-outer-spin-button,
  input[type="number"]::-webkit-inner-spin-button {
      -webkit-appearance: none;
      margin: 0;
  }
  input[type="email"] {
    width: 28vw;
  }
</style>