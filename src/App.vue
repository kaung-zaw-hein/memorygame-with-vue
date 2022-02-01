<template>
<div class="container">
   <header>
          <img src="./assets/Brnyr-logos_transparent.png" alt="">
  </header>
  <Items @result="results"></Items>
  <Result :res="res" @reset="reset"></Result>
</div>
</template>

<script>

import Items from './components/Items'
import Result from './components/Result'
import {ref} from '@vue/reactivity'
export default {
  name: 'App',
  components: {
    Items,
    Result,
  },
  setup(){
    const res = ref([]);
    const state = ref(false);
    let results = (a) => {
      res.value.push(...a);
    }
    let reset = () =>{
      res.value=[];
      location.reload();
    }
    return {results,res,reset,state}
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
