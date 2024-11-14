<script setup>
  import RowBar from './RowBar.vue'
  defineProps({
    win_percentages: {
      type: Array,
      required: true
    }
  })
</script>

<template>
  <div class="leftalign">
    <RowBar name="Player" description="Win Percentage" evenodd="even" topbottom="top"/>
    <RowBar
        v-for="(player,index) in win_percentages"
        :name="player[0]"
        :description="String(player[1] + '%')"
        :evenodd="index % 2 === 1 ? 'even' : 'odd'"
        :topbottom="index === win_percentages.length-1 ? 'bottom' : ''"
      />
  </div>
</template>
