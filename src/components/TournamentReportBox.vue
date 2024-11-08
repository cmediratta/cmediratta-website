<script setup>
  import InputField from './molecules/InputField.vue'
  import DropdownMenu from './molecules/DropdownMenu.vue'
  import { ref } from 'vue'
  const rds = [1, 2, 3, 4, 5]
  var tournament_divisions = ref([])
  const t_id = ref('')
  const current_div = ref('')
  const num_rounds = ref(0)
  const email = ref('')
  var state = ref('input')
  var win_percentage = []
  var win_avg = []

  async function setDivisions() {
    const response = await sendRequest('get-divisions', JSON.stringify({ t_id: String(t_id.value) }))
    console.log(response.message)
    tournament_divisions.value = response.message
  }

  async function getData() {
    state.value = 'loading'
    const payload = {
                t_id: String(t_id.value),
                email: email.value,
                rounds: num_rounds.value,
                current_div: current_div.value
              }
    console.log(payload)
    
    var msg = await sendRequest('generate-report', JSON.stringify(payload))

    state.value = 'display'
    win_percentage = msg.sorted_win_percentage
    win_avg = msg.win_avg
  }

  async function sendRequest(destination, contents) {
    var response = await fetch('http://127.0.0.1:5000/' + destination, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: contents
    });

    var data = await response.json()

    return data
  }

</script>

<template>
  <form @submit.prevent="handleSubmit" v-if="state==='input'">
    <div>
      <label>Input Tournament ID:</label>
      <img src="../assets/tour_id_image.jpg"></img>
    </div>
    <InputField type="number" class="tournament-id" Child v-model="t_id"/>
    <button @click="setDivisions">Get Divisions</button>
    <div v-show="tournament_divisions.length>0">
      <DropdownMenu :options="tournament_divisions" placeholder="Select Division" v-model="current_div"/>
      <DropdownMenu :options="rds" placeholder="# of Rounds" v-model="num_rounds"/>
      <label>E-mail: </label>
      <InputField type="email" class="" Child v-model="email"/>
      <button @click="getData">Submit </button>
    </div>
  </form>
  <div v-else-if="state==='loading'">
    Loading Data
  </div>
  <div v-else-if="state==='display'">
    {{ win_avg }}
    {{ win_percentage }}
  </div>
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
    cursor: pointer;
  }
  .newline {
    margin: 1.5vh 0;
  }
</style>
