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
    url: {
      type: String,
      required: true
    }
  })
</script>

<template>
  <RouterLink :to="url" class="project-link">
    <div class="project-item">
      <h3 class="project-title"> {{ name }}</h3>
      <hr class="divider">
      <p class="project-description">{{ description }}</p>
    </div>
  </RouterLink>
</template>

<style>
  .project-item {
    background-color: #fff;
    border: 2px solid #e0e0e0;
    border-radius: 8px;
    padding: 20px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    cursor: pointer;
    text-align: center;
    color: #333;
    transition: transform 0.3s, box-shadow 0.3s;
  }

  .project-item:hover {
    transform: scale(1.03);
    box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);    
  }
  .project-title {
    font-size: 1.2em;
    margin: 0;
    color: #333;
  }

  .divider {
    width: 60%;
    margin: 10px auto;
    border: none;
    border-top: 2px solid #e0e0e0;
  }

  .project-description {
    font-size: 0.9em;
    color: #666;
    margin-top: 10px;
  }

  .project-link {
    width: 100%;
    display: block;
    text-decoration: none;
    color: inherit;
  }
</style>
