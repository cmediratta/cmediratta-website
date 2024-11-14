<template>
  <ul class="menu">
    <nav>
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/projects">Projects</RouterLink>
      <RouterLink to="/about">About</RouterLink>
    </nav>
  </ul>
</template>

<style scoped>
  ul.menu {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    width: 100%;
    margin-top:0px;
    font-size: 2.5vw;
    z-index: 1000;
    background-color: var(--vt-c-black-mute);
  }
  nav {
    list-style: none;
    display: inline-block;
    color: white;
    padding: 2vh 2vh;
  }

  nav a.router-link-exact-active {
    color: var(--color-text);
  }

  nav a.router-link-exact-active:hover {
    background-color: transparent;
  }

  nav a {
    display: inline-block;
    padding: 0 1rem;
    border-left: 1px solid var(--color-border);
  }
</style>