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
</style>
