<script setup>
  const SERVER = 'https://server.cmediratta.com/'
  import InputField from './molecules/InputField.vue'
  import DropdownMenu from './molecules/DropdownMenu.vue'
  import PlayerTable from './molecules/PlayerTable.vue'
  import { ref } from 'vue'
  const rds = [1, 2, 3, 4, 5]
  var tournament_divisions = ref([])
  const t_id = ref('')
  const current_div = ref('')
  const num_rounds = ref(0)
  const email = ref('')
  var state = ref('input')
  const win_percentages = ref([])
  var win_avg
  var cash_avg

  async function setDivisions() {
    const response = await sendRequest('get-divisions', JSON.stringify({ t_id: String(t_id.value) }))
    console.log(response.message)
    tournament_divisions.value = response.message
  }

  async function getData() {
    state.value = 'loading'
    const payload = {
                t_id: String(t_id.value),
                rounds: num_rounds.value,
                current_div: current_div.value
              }
    console.log(payload)
    
    var msg = await sendRequest('generate-report', JSON.stringify(payload))

    state.value = 'display'
    win_percentages.value = msg.sorted_win_percentage
    win_avg = msg.win_avg
    cash_avg = msg.cash_avg
    console.log(win_percentages.value)
  }

  async function sendRequest(destination, payload) {
    var response = await fetch(SERVER + destination, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: payload
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
      <button @click="getData">Submit </button>
    </div>
  </form>
  <div v-else-if="state==='loading'">
    Loading Data (Should be about 2 players per second)
  </div>
  <div v-else-if="state==='display'" class="display-container">
    <PlayerTable :win_percentages="win_percentages"/>
    <div class="stats-container">
      <div>Average Winning Rating: {{ win_avg }}</div>
      <div>Average Cash Line Rating: {{ cash_avg }}</div>
    </div>
  </div>
</template>


<style scoped>
  .display-container {
    display: flex;
    gap: 2vw;
  }
  .stats-container {
    display: flex;
    flex-direction: column;
    align-self: flex-start;
    padding: 2vh;
    background-color: #f0f0f0;
    border-radius: 1vh;
    width: 20vw;
    font-size: 1.2vw;
    color: black;
  }
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
  .background {
    background-color: blue;
    width: 80vw;
  }
</style>
