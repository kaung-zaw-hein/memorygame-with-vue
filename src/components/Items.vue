<template>
     <div>
       <section class="score-panel">
          <ul class="stars">
            <li v-for=" n in stars" :key="n"><i class="fa fa-star"></i></li>
          </ul>
      
          <span class="moves" >{{moves}}</span> 
      
          <div class="timer">
          </div>
      
          <div class="restart" onclick=startGame()>
            Reset
            <i class="fa fa-repeat"></i>
          </div>
        </section>
      
        <ul class="deck" id="card-deck">
          <li class="card" :type="card.type"
          v-for="card in cards" :key="card" 
          @click.prevent="displayCard"
          :class="{'disabled': card.disabled, 'match': card.match,'unmatched': card.unmatched,'open': card.open, 'show': card.show}"
          >
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
import {ref,onBeforeUpdate, onUpdated } from '@vue/reactivity';
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
       type: "atom", 
       class: "fas fa-atom"
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
  cards.value.forEach((card) => {
    card.disabled = false;
		card.match = false;
    card.unmatched = false;
    card.show = false;
    card.open = false;
  });
  const	openedCards  =  ref([]);
  const index = ref([]);
  const cardOpen = (event) => {
    const parent = event.target.parentNode;
    index.value.push(Array.prototype.indexOf.call(parent.children, event.target));
    openedCards.value.push(event.target);
    const len = openedCards.value.length;
    if(len == 2){
      moveCounter();

      if(openedCards.value[0].type === openedCards.value[1].type){
        matched();
      }else{
        unmatched(index);
      }
    }
  };
  const matchCard =ref([]);
  const matched = () => {
    cards.value.forEach( (card) => {
      if(openedCards.value[0].type === card.type){
        card.match = true;
      }
    })
    openedCards.value[0].match = true;
    openedCards.value[1].match = true;
    openedCards.value[0].classList.remove("show", "open");
    openedCards.value[1].classList.remove("show", "open");
    matchCard.value.push(openedCards.value[1].type);
    openedCards.value = [];
    index.value =[];
  };

  const unmatched= ((index) => {
      disable();

      for (let i = 0; i < index.value.length; i++) {
        cards.value[index.value[i]].unmatched = true;
        cards.value[index.value[i]].show = true;
        cards.value[index.value[i]].open = true;
      }

      setTimeout(function() {
        
        enable();
        openedCards.value = [];
        index.value =[];
      }, 900);
  })
  // disable cards temporarily
  const disable = () => {
    cards.value.forEach( card => {
      card.disabled = true
    });
  }

  //enable cards and disable matched cards
  const enable = () => {
    cards.value.forEach( card => {
      card.disabled = false;
      card.unmatched = false;
      card.open = false;
      card.show = false;
       for (let i = 0; i < matchCard.value.length; i++) {
        if(matchCard.value[i] === card.type){
          card.disabled = true;
          card.open = true;
          card.show = true;
        }
      }
    });
  }

  const displayCard = (event) => {
    event.target.classList.toggle("open");
    event.target.classList.toggle("show");
    event.target.classList.toggle("disabled");
    cardOpen(event);
  }

  const moves = ref("0 move");
  const move = ref(0);
  const stars = ref(5);
  const moveCounter = () => {
    move.value++
    moves.value = move.value + 'moves'

    //stars rating
    if(move.value>18){
      stars.value = 1;
    }else if (move.value>15){
      stars.value = 2;
    }else if (move.value>13){
      stars.value = 3;
    }else if (move.value>10){
      stars.value = 4;
    }else{
      stars.value=5;
    }
    
  }
 




   return {cards,cardsType,displayCard,openedCards,cardOpen,matchCard,matched,unmatched,disable,enable,index,moves,moveCounter,stars};
 }
 
}
</script>

<style>

</style>