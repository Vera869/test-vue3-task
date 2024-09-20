<template>
<div class="filter" :style="`background-color: ${options.color}`">
   <v-tooltip class="tooltip" text="По возрастанию рейтинга">
      <template v-slot:activator="{ props }">
         <button 
            v-bind="this.button" 
            id="up" 
            class="filter__button filter__button_up" 
            @click="hendleSort($event.target)" 
            :style="`box-shadow: 0px 0px 27px 0px ${borderColor}`"
         ></button>
         <!-- disabled="isBtnDisabled"  $event.target.id-->
      </template>
   </v-tooltip>
   <v-tooltip text="По убыванию рейтинга">
      <template v-slot:activator="{ props }">
         <button 
            v-bind="this.button" 
            id="down" 
            class="filter__button filter__button_down" 
            @click="hendleSort($event.target)"
            :style="`box-shadow: 0px 0px 27px 0px ${borderColor}`"
         ></button>
      </template>
   </v-tooltip>
   <v-tooltip text="Без сортировки">
      <template v-slot:activator="{ props }">
         <button 
            v-bind="this.button" 
            id="nosort" class="filter__button filter__button_nosort" 
            @click="hendleSort($event.target)" 
            :style="`box-shadow: 0px 0px 27px 0px ${borderColor}`"
         ></button>
      </template>
   </v-tooltip>
</div>
</template>

<script setup>
import { computed, inject, ref } from 'vue';

const firstList = inject('firstList');
const secondList = inject('secondList');
const lastList = inject('lastList');
// let isBtnDisabled = ref(false);

const borderColor = computed(() => {
    return props.options.id === 1 ? 'blue' : props.options.id === 2 ? 'yellow' : 'pink';
  });
const props = defineProps({
   options: {},
});
const hendleSort = (event) => {
   const id = event.id;
   let cards = ref([]);
   console.log(id);
   function getLocalCards() {
   switch (props.options.id) {
      case 1:
         cards = firstList;
         break;
      case 2:
         cards = secondList;
         break;
      case 3:
         cards = lastList;
         break;
      }
   }
   getLocalCards();
   if(id === "up") {cards = cards.value.sort((a, b) => a.rating.rate - b.rating.rate);}
   else if(id === "doun") {cards = cards.value.sort((a, b) => b.rating.rate - a.rating.rate);}
   else if(id === "nosort") {cards = cards;}
   console.log(cards);
}

</script>

<style lang="scss" scoped>
.filter {
   width: 400px;
   height: 80px;
   display: grid;
   grid-template-columns: repeat(3, 1fr);
   justify-items: center;
   column-gap: 5px;
   align-content: center;
   border-radius: 10px;
   padding: 5px;
   margin-bottom: 10px;
   .filter__button {
      width: 55%;
      height: 55px;
      border-radius: 10px;
      background-color: rgb(255, 255, 255);
      padding: 3px;
      &:hover {
         box-shadow: transparent;
      }
      &:active {
         background-color: transparent;
      }
      &:disabled {
         background-color: transparent;
         box-shadow: none;
      }
   }
   .filter__button_up {
      background-image: url(../assets/icon-sort-up.png);
      background-size: 50px 50px;
      background-repeat:no-repeat;
      background-position: center center;
   }
   .filter__button_down {
      background-image: url(../assets/icon-sort-down.png);
      background-size: 50px 50px;
      background-repeat:no-repeat;
      background-position: center center;
   }
   .filter__button_nosort {
      background-image: url(../assets/icon-clear.png);
      background-size: 50px 50px;
      background-repeat:no-repeat;
      background-position: center center;
   }
}
</style>