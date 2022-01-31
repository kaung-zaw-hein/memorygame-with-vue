<template>
<div class="container">
   <header>
          <img src="./assets/Brnyr-logos_transparent.png" alt="">
  </header>
  <Items></Items>
  <Result></Result>
</div>
</template>

<script>

import Items from './components/Items'
import Result from './components/Result'
export default {
  name: 'App',
  components: {
    Items,
    Result,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #ffffff;
}
::-webkit-scrollbar {
  width: 5px;
}
::-webkit-scrollbar-track {
  box-shadow: inset 5px 0 5px rgba(48, 151, 182, 0.5); 
  border-radius: 10px;
}
::-webkit-scrollbar-thumb {
  background: #13acc0; 
  border-radius: 10px;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: #10bdd4; 
}
</style>
