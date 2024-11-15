<script setup>
  const SERVER = 'https://server.cmediratta.com/'
  import InputField from './molecules/InputField.vue'
  import DropdownMenu from './molecules/DropdownMenu.vue'
  import PlayerTable from './molecules/PlayerTable.vue'
  import ErrorBar from './molecules/ErrorBar.vue'
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
  var error_msg = ''
  const error_bar = ref(false)

  async function handleErrorMessage(code) {
    error_bar.value = true
    switch (code) {
      case 555:
        error_msg = "Tournament in progress/already finished."
        break
      case 556:
        error_msg = "Tournament does not exist."
        break
      default:
        error_msg = "Unknown Error."
    }
  }

  async function setDivisions() {
    error_bar.value = false
    const msg = await sendRequest('get-divisions', JSON.stringify({ t_id: String(t_id.value) }))
    if (msg==0) {
      return
    }
    tournament_divisions.value = msg.tournament_divisions
  }

  async function getData() {
    error_bar.value = false
    state.value = 'loading'
    const payload = {
                t_id: String(t_id.value),
                rounds: num_rounds.value,
                current_div: current_div.value
              }
    const msg = await sendRequest('generate-report', JSON.stringify(payload))
    if(msg==0){
      return
    }

    state.value = 'display'
    win_percentages.value = msg.sorted_win_percentage
    win_avg = msg.win_avg
    cash_avg = msg.cash_avg
  }

  async function sendRequest(destination, payload) {
    var response = await fetch(SERVER + destination, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: payload
    });

    const code = await response.status

    if (code!=200) {
      handleErrorMessage(code)
      return 0
    }

    return await response.json()
  }

</script>

<template>
  <form @submit.prevent="" v-if="state==='input'">
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
  <ErrorBar :error_msg="error_msg" v-show="error_bar"/>
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
