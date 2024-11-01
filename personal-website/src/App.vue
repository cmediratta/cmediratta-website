<script setup>
import { RouterLink, RouterView } from 'vue-router'
import MenuBar from './components/MenuBar.vue'
</script>

<template>
  <MenuBar />

  <RouterView class="content"/>
</template>

<style scoped>
  .content {
    padding-top: 7vh;
  }
</style>
