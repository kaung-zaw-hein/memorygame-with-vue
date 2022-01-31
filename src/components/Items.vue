<template>
     <div>
       <section class="score-panel">
          <ul class="stars">
            <li><i class="fa fa-star"></i></li>
            <li><i class="fa fa-star"></i></li>
            <li><i class="fa fa-star"></i></li>
          </ul>
      
          <span class="moves">0 Move</span> 
      
          <div class="timer">
          </div>
      
          <div class="restart" onclick=startGame()>
            Reset
            <i class="fa fa-repeat"></i>
          </div>
        </section>
      
        <ul class="deck" id="card-deck">
          <li class="card" :type="card.type"
          v-for="card in cards" :key="card" @click.prevent="displayCard">
            <i :class="card.class"></i>
          </li>
          <!-- <li class="card" type="fan">
            <i class="fas fa-fan"></i>
          </li>
          <li class="card match" type="pickup">
            <i class="fas fa-truck-pickup"></i>
          </li>
          <li class="card" type="bolt">
            <i class="bolt"></i>
          </li>
          <li class="card" type="cube">
            <i class="fa fa-cube"></i>
          </li>
          <li class="card match" type="pickup">
            <i class="fas fa-truck-pickup"></i>
          </li>
          <li class="card" type="cardboard">
            <i class="fas fa-vr-cardboard"></i>
          </li>
          <li class="card" type="bicycle">
            <i class="fa fa-bicycle"></i>
          </li>
          <li class="card" type="artstation">
            <i class="fab fa-artstation"></i>
          </li>
          <li class="card" type="tractor">
            <i class="fas fa-tractor"></i>
          </li>
          <li class="card" type="cardboard">
            <i class="fas fa-vr-cardboard"></i>
          </li>
          <li class="card" type="tractor">
            <i class="fas fa-tractor"></i>
          </li>
          <li class="card open show" type="bolt">
            <i class="fa fa-bolt"></i>
          </li>
          <li class="card" type="bicycle">
            <i class="fa fa-bicycle"></i>
          </li>
          <li class="card" type="fan">
            <i class="fas fa-fan"></i>
          </li>
          <li class="card" type="cube">
            <i class="fa fa-cube"></i>
          </li> -->
        </ul>
     </div>
</template>

<script>
import {ref, onMounted } from '@vue/reactivity';
export default {
 setup(){
   
  const _ = require('lodash');
  const cardsType = ref([
     {
       type: "artstation", 
       class: "fab fa-artstation"
     },
      {
       type: "fan", 
       class: "fas fa-fan"
     },
      {
       type: "pickup", 
       class: "fas fa-truck-pickup"
     },
      {
       type: "cardboard", 
       class: "fas fa-vr-cardboard"
     },
      {
       type: "bolt", 
       class: "bolt"
     },
      {
       type: "cube", 
       class: "fa fa-cube"
     },
      {
       type: "tractor", 
       class: "fas fa-tractor"
     },
      {
       type: "bicycle", 
       class: "fa fa-bicycle"
     },
   ]);
  const cards=  ref([].concat(_.cloneDeep(cardsType.value), _.cloneDeep(cardsType .value)));
  cards.value = _.shuffle(cards.value) 
  console.log(cards.value);
   return {cards,cardsType};
 }
 
}
</script>

<style>

</style>