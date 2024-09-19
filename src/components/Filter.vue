<template>
<div class="filter" :style="`background-color: ${options.color}`">
   <button class="filter__button filter__button_up"></button>
   <button class="filter__button filter__button_down"></button>
   <button class="filter__button filter__button_nosort"></button>
</div>
</template>

<script setup>
  const props = defineProps({
    options: {},
  });
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
   color: #fff;
   // background-color: blue;
   padding: 5px;
   margin-bottom: 10px;
}
   .filter__button {
      width: 55%;
      height: 55px;
      // min-height: 30px;  ${borderColor}
      border-radius: 10px;
      background-color: rgb(255, 255, 255);
      padding: 3px;
      &:hover {
         box-shadow: 0px 0px 27px 0px borderColor;
      }
      &:active {
         background-color: blue;
      }
      &:disabled {
         background-color: blue;
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
      background-image: url(../assets/icon-nosort.png);
      background-size: 50px 50px;
      background-repeat:no-repeat;
      background-position: center center;
   }
// }

</style>