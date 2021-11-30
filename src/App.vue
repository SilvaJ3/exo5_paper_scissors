<template>
  <div id="app" class="relative" :class="[showModal === true ? 'bg-gray-700' : '']">
    <div v-if="showModal" class="backdrop" @click="showModal = false">
      <div class="rounded-md w-96 h-96 flex flex-col border border-white bg-white p-4 modal">
        <div class="flex justify-between items-center mb-6">
          <h1 class="text-xl">RULES</h1>
          <img src="../public/images/icon-close.svg" alt="" class="h-4 cursor-pointer" @click="showModal = false">
        </div>
        <div class="flex justify-center items-center">
          <img src="../public/images/image-rules.svg" alt="">
        </div>
      </div>
    </div>
    <div class="flex flex-col justify-center items-center w-full">
      <!-- Affichage score -->
      <div class="flex justify-between items-center w-2/5 rounded-md border border-white px-3 py-2">
        <div class="text-white">
          <h1 class="font-bold text-xl">ROCK</h1>
          <h1 class="font-bold text-xl">PAPER</h1>
          <h1 class="font-bold text-xl">SCISSORS</h1>
        </div>
        <div class="rounded-md bg-white py-2 px-6 flex flex-col justify-center items-center">
          <span>SCORE</span>
          <h1 class="text-4xl font-bold">{{score}}</h1>
        </div>
      </div>

      <!-- Tableau de jeu -->
      <div class="board mt-10 w-1/2 h-96" v-if="!inGame">
        <div class="flex justify-evenly">
          <div id="paper" class="rounded-full px-5 py-4 bg-white paper shadow-inner" @click="selection($event)">
            <img src="../public/images/icon-paper.svg" alt="icon-paper">
          </div>
          <div id="scissors" class="rounded-full px-5 py-4 bg-white scissors shadow-inner" @click="selection($event)">
            <img src="../public/images/icon-scissors.svg" alt="icon-scissors">
          </div>
        </div>
        <div class="flex justify-center mt-32">
          <div id="rock" class="rounded-full px-5 py-4 bg-white rock shadow-inner" @click="selection($event)">
            <img src="../public/images/icon-rock.svg" alt="icon-rock">
          </div>
        </div>
      </div>

      <!-- Resultats -->

      <div v-else class="flex w-full h-96 mt-10">
        <div class="flex flex-col justify-center" :class="timerOut === true ? 'w-1/3 items-end' : 'w-1/2 items-center'">
          <h1 class="text-white mb-10">YOU PICKED</h1>
          <div v-if="player === 'paper'" class="rounded-full px-5 py-4 bg-white paper shadow-inner">
            <img src="../public/images/icon-paper.svg" alt="icon-paper">
          </div>
          <div v-else-if="player === 'scissors'" class="rounded-full px-5 py-4 bg-white scissors shadow-inner">
            <img src="../public/images/icon-scissors.svg" alt="icon-scissors">
          </div>
          <div v-if="player === 'rock'" class="rounded-full px-5 py-4 bg-white rock shadow-inner">
            <img src="../public/images/icon-rock.svg" alt="icon-rock">
          </div>
        </div>
        <div class="w-1/3 flex flex-col justify-center items-center" v-if="timerOut">
          <h1 class="text-white text-4xl mb-5">{{result}}</h1>
          <div class="rounded-md bg-white py-2 px-8 cursor-pointer" @click="reset()">
            <h1>PLAY AGAIN</h1>
          </div>
        </div>
        <div class="flex flex-col justify-center" :class="timerOut === true ? 'w-1/3 items-start' : 'w-1/2 items-center'">
          <h1 class="text-white mb-10">THE HOUSE PICKED</h1>
          <div v-if="house === ''">
            <div class="rounded-full px-5 py-4 empty w-28 h-28 shadow-inner">
              
            </div>
          </div>
          <div v-else>
            <div v-if="house === 'paper'" class="rounded-full px-5 py-4 bg-white paper shadow-inner">
              <img src="../public/images/icon-paper.svg" alt="icon-paper">
            </div>
            <div v-else-if="house === 'scissors'" class="rounded-full px-5 py-4 bg-white scissors shadow-inner">
              <img src="../public/images/icon-scissors.svg" alt="icon-scissors">
            </div>
            <div v-if="house === 'rock'" class="rounded-full px-5 py-4 bg-white rock shadow-inner">
              <img src="../public/images/icon-rock.svg" alt="icon-rock">
            </div>
          </div>
        </div>
      </div>

    </div>


      <!-- Rules -->
      <div class="flex justify-end">
        <div class="rounded-md border border-white px-4 py-1 cursor-pointer" @click="toggleRules()">
          <h1 class="text-white">RULES</h1>
        </div>
      </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      score: 12,
      showModal: false,
      inGame: false,
      choice: ["paper", "scissors", "rock"],
      player: "",
      house: "",
      timerOut: false,
      result: "",
    }
  },
  methods: {
    toggleRules() {
      this.showModal = !this.showModal;
    },
    selection(event) {
      this.inGame = true;
      if (event.target.id == "paper") {
        this.player = event.target.id;
      } else if (event.target.id == "scissors"){
        this.player = event.target.id;
      } else {
        this.player = event.target.id;
      }
      let random = Math.floor((Math.random() * 3));


      setTimeout(() => {
        this.house = this.choice[random];
        if (this.player === this.house) {
          this.result = "It's a draw";
          this.timerOut = true;
        } else if (this.player === "paper") {
          if (this.house === "rock") {
            this.result = "YOU WIN";
            this.score++;
            this.timerOut = true;
          } else {
            this.result = "YOU LOSE";
            this.score--;
            this.timerOut = true;
          }
        } else if (this.player === "scissors") {
          if (this.house === "paper") {
            this.result = "YOU WIN";
            this.score++;
            this.timerOut = true;
          } else {
            this.result = "YOU LOSE";
            this.score--;
            this.timerOut = true;
          }
        } else if (this.player === "rock") {
          if (this.house === "scissors") {
            this.result = "YOU WIN";
            this.score++;
            this.timerOut = true;
          } else {
            this.result = "YOU LOSE";
            this.score--;
            this.timerOut = true;
          }
        }
      }, 2000);

    },
    reset() {
      this.timerOut = false;
      this.inGame = false;
      this.house = "";
      this.result = "";
    }
  },
}

</script>

<style>
#app {
  font-family: 'Barlow Semi Condensed', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  padding: 5% 5% 1% 5%;
}

body {
  /* padding: 5%; */
  background-color: #1f3756;
  margin: 0;
  box-sizing: border-box;
}

.backdrop {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.562);
  z-index: 1;
}

.modal {
  position: absolute;
  top: 25%;
  left: 37%;
  z-index: 2;
}

.board{
  background-image: url("../public/images/bg-triangle.svg");
  background-repeat: no-repeat;
  background-position: center;
}

.paper, .scissors, .rock {
  cursor: pointer;
}

.paper img, .scissors img, .rock img {
  pointer-events: none;
}

.paper {
  border: solid 10px hsl(230, 89%, 62%);
}

.scissors {
  border: solid 10px hsl(39, 89%, 49%);
}

.rock {
  border: solid 10px hsl(349, 70%, 56%);
}

.empty {
  background-color:hsl(237, 49%, 15%);
}

</style>
