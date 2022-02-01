<template>
  <div id="popup1" class="overlay"
        :class="{'show' : results.length>1}">
          <div class="popup">
            <h2>Congratulations 🎉</h2>
            <a class="close" @click.prevent="reset" href=#>×</a>
            <div class="content-1">
              Congratulations you're a winner 
            </div>
            <div class="content-2">
              <p>You made <span id=finalMove>{{results[1]}}</span> moves </p>
              <p>in <span id=totalTime>{{results[3]}} </span> </p>
              <p>Rating:
                 <span id=starRating v-for=" n in results[2]" :key="n">
                   <i class="fa fa-star"></i></span></p>
            </div>
            <button id="play-again"  @click.prevent="reset">
              Play again 
            </button>
          </div>
    </div>
</template>

<script>
import {ref} from '@vue/reactivity'
export default {
  props: ['res'],
  setup(props,context){
    const results = ref(props.res);
    const reset = () => {
      results.value = ""
      context.emit('reset')
    }
    return {
      results,reset}
  }

}
</script>

<style>

</style>