<script setup>
  import InputField from './molecules/InputField.vue'
</script>

<template>
  <form>
    <label>Input Tournament ID:</label>
    <InputField type="number" class="tournament-id" />
    <button>Get Divisions</button>
    <label v-show="false">E-mail: </label>
    <InputField type="email" class="" v-show="false"/>
    <button v-show="false">Submit</button>
  </form>
</template>


<style scoped>
  form {
    margin: 3vh auto;
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
    padding: 3vh;
    margin: 3vh 0;
    border: 0.3vh solid #ccc;
    border-radius: 2vh;
    font-size: 1.7vw; 
  }
  button {
    background-color: hsla(160, 100%, 37%, 1);
  }

</style>
