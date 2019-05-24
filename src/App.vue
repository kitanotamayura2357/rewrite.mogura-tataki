<template>
  <div class="whackamole">
    <h1 class="logo">
      Whack-a-mole!
    </h1>
    <button
      class="start-game"
      v-on:click="startGame"
      v-on:whack="handleMoleWhack"
    >
      Start Game
    </button>
    <div class="counters-container">
      <Counter label="Score:" v-bind:value="score"></Counter>
      <Counter label="High-Score:" v-bind:value="highscore"></Counter>
      <Counter label="Timer" v-bind:value="timer"></Counter>
    </div>
    <Moles
    v-bind:moleData="moles"
    v-bind:gameActive="gameActive"
    v-on:whack="handleMoleWhack"
    />
  </div>
</template>

<script>
import Counter from './components/Counter';
import Moles from './components/Moles';

export default {
  name: 'App',
  components: { 
    Counter, // "Counter": Counter,
    Moles // "Moles": Moles,
  },
  data: function() {
    return{
      score: 10,
      highscore: 0,
      timer: 20,
      moles: [false, false, false, false],
      gameActive: false,
    };
  },

  methods: {
    resetState: function() {
      this.score = 0;
      this.timer = 20;
      this.moles = [false,false,false,false];
    },
    startGame: function() {
      this.resetState();
      this.gameActive = true;
      this.startTimer();
    },
    endGame: function() {
      this.gameActive = false;
      this.stopTimer();
    },
    startTimer: function() {
      this.timerId = setInterval(() => {
        this.decrementTime();
      }, 1000);
    },
    decrementTime: function() {
      this.timer--;
      if (this.timer === 0) {
        this.endGame();
      }
    },
    stopTimer: function() {
      clearInterval(this.timerId);
    },
    handleMoleWhack: function(moleId) {
      console.log('moleId  = ', moleId)
    }
  },
};
</script>

<style>
.whackamole {
  font-family: 'Bungee', sans-serif;
  max-width: 960px;
  margin: auto;
  text-align: center;
}

.start-game {
  font-family: 'Bungee', sans-serif;
  padding: 20px;
  border-radius: 3px;
  border: 0;
  background-color: #52b1d6;
  color: #fff;
  font-size: 1em;
  cursor: pointer;
}

.counters-container {
  display: flex;
  justify-content: space-evenly;
}

.mole-container.active .mole {
  /* display: block; */
  top: 0px;
}


</style>
