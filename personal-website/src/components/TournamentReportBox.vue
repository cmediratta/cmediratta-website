<script setup>
  import InputField from './molecules/InputField.vue'
  import DropdownMenu from './molecules/DropdownMenu.vue';
  var tournament_divisions = ['MPO', 'MA1', 'MA2', 'MA3', 'FPO', 'FA1', 'FA2', 'FA3', 'MP40', 'MP50', 'MP60', 'MP70', 'FP40', 'FP50', 'FP60', 'FP70'];
</script>

<template>
  <form>
    <div>
      <label>Input Tournament ID:</label>
      <img src="../assets/tour_id_image.jpg"></img>
    </div>
    <InputField type="number" class="tournament-id" />
    <button>Get Divisions</button>
    <div v-show="tournament_divisions.length>0">
      <DropdownMenu :options="tournament_divisions" placeholder="Select Division"/>
      <label>E-mail: </label>
      <InputField type="email" class="" />
      <button>Submit </button>
    </div>
  </form>
</template>


<style scoped>
  form {
    text-align: left;
    padding: 4vh;
    border-radius: 3vh;
    background: var(--vt-c-white-mute);
    color: var(--vt-c-black-mute);
  }
  label {
    font-size: 1.7vw;
  }
  input, 
  textarea, 
  select, 
  button {
    width: 100%;
    padding: 2vh;
    margin: 3vh 0;
    border: 0.3vh solid #ccc;
    border-radius: 2vh;
    font-size: 1.7vw; 
  }
  button {
    background-color: hsla(160, 100%, 37%, 1);
  }
  .newline {
    margin: 1.5vh 0;
  }
</style>
