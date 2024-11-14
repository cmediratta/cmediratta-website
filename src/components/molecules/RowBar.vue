<script setup>
  defineProps({
    name: {
      type: String,
      required: true
    },
    description: {
      type: String,
      required: true
    },
    evenodd: {
      type: String,
      required: true
    },
    topbottom: {
      type: String,
      required: false
    }
  })
</script>

<template>
  <div :class="['row-bar', evenodd, topbottom]">
    <div class="cell name">{{ name }}</div>
    <div class="cell description">{{ description }}</div>
  </div>
</template>


<style scoped>
  .row-bar {
    display: flex;
    padding: 0.5vw;
    border-bottom: 1px solid #ccc;
    color: black;
    width: 50vw;
    font-size: 1.5vw;
  }
  .cell {
    flex: 1;
    padding: 0.5vh;
  }
  .even {
    background-color: #f9f9f9;
  }
  .odd {
    background-color: #ffffff;
  }
  .top {
    border-top-left-radius: 2.5vh;
    border-top-right-radius: 2.5vh;
  }
  .bottom {
    border-bottom-left-radius: 2.5vh;
    border-bottom-right-radius: 2.5vh;
  }
</style>