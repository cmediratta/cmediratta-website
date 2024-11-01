<template>
  <div class="dropdown">
    <div @click="toggleDropdown" class="dropdown-toggle">
      {{ selected || placeholder }}
    </div>
    <ul v-if="isOpen" class="dropdown-menu">
      <li
        v-for="(option, index) in options"
        :key="index"
        @click="selectOption(option)"
        class="dropdown-item"
      >
        {{ option }}
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: "Dropdown",
    props: {
      options: {
        type: Array,
        required: true
      },
      placeholder: {
        type: String,
        default: "Select an option"
      }
    },
    data() {
      return {
        isOpen: false,
        selected: null
      };
    },
    methods: {
      toggleDropdown() {
        this.isOpen = !this.isOpen;
      },
      selectOption(option) {
        this.selected = option;
        this.isOpen = false;
        this.$emit("select", option);
      }
    }
  };
</script>
  
<style scoped>
  .dropdown {
    position: relative;
    width: 200px;
  }
  
  .dropdown-toggle {
    width: 100%;
    padding: 10px;
    width: 100%;
    margin: 1.5vh 0;
    border: 0.3vh solid #ccc;
    background-color: #fff;
    border-radius: 2vh;
    font-size: 1.7vw; 
    cursor: pointer;
  }
  
  .dropdown-menu {
    position: absolute;
    width: 100%;
    margin: -1.5vh 0;
    padding: 0;
    list-style: none;
    border: 1px solid #ccc;
    border-radius: 5px;
    background-color: #fff;
    max-height: 150px;
    overflow-y: auto;
    z-index: 10;
    font-size: 1.7vw;
  }
  
  .dropdown-item {
    padding: 1vh;
    cursor: pointer;
  }
  
  .dropdown-item:hover {
    background-color: #f0f0f0;
  }
</style>