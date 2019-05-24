<template>
<div v-bind:class="classNames">
    <Mole
        v-for="(moleState, idx) in moleData"
        v-bind:key="idx"
        v-bind:active="moleState"
    >
    </Mole>
</div>
</template>

<script>
 import Mole from './Mole';
 export default {
     name: 'Moles',
     components:{
         Mole,
     },
     props: ['moleData', 'gameActive'],
     computed: {
         classNames: function() {
             return {
                 'moles-container': true,
                 'game-active': this.gameActive,
             };
         }
     },
 };
</script>

<style>
.moles-container.game-active {
  opacity: 1;
}

.moles-container {
  margin-top: 20px;
  display: flex;
  justify-content: space-between;
  opacity: 0.9;
  transition: opacity 0.3s ease;
}
</style>