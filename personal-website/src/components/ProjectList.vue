<script setup>
  import ProjectItem from './molecules/ProjectItem.vue'
  const projects = [
    { name: "Disc Golf Tournament Report",
      description: "This project scrapes the PDGA Website to gain player information in order\
                    to inform the chances for victory of each player and the expected strength\
                    of the winning round.",
      url: "/projects/tournament-report" },
  ]
</script>

<template>
  <div class="project-list">
    <ProjectItem
      v-for="(project, index) in projects"
      :key="index"
      :name="project.name"
      :description="project.description"
      :url="project.url"
    />
  </div>
</template>


<style>
  .project-list {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 3vh;
    width: 80%;
    margin: 0 auto 3vw auto;
    z-index: 0;
  }
</style>
