<template>
  <div id="app" class="relative" :class="[showModal === true ? 'bg-gray-700' : '']">
    <div v-if="showModal" class="backdrop">
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
      <div class="board mt-10 w-1/2 h-96">
        <div class="flex justify-evenly">
          <div class="rounded-full px-5 py-4 bg-white paper shadow-inner">
            <img src="../public/images/icon-paper.svg" alt="icon-paper">
          </div>
          <div class="rounded-full px-5 py-4 bg-white scissors shadow-inner">
            <img src="../public/images/icon-scissors.svg" alt="icon-scissors">
          </div>
        </div>
        <div class="flex justify-center mt-32">
          <div class="rounded-full px-5 py-4 bg-white rock shadow-inner">
            <img src="../public/images/icon-rock.svg" alt="icon-rock">
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
      showModal: true,
    }
  },
  components: {
  },
  methods: {
    toggleRules() {
      this.showModal = !this.showModal;
    }
  }
}
</script>

<style>
#app {
  font-family: 'Barlow Semi Condensed', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  padding: 5%;
  background-color: #1f3756;
}

body {
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
}

.modal {
  position: absolute;
  top: 25%;
  left: 37%;
}

.board{
  background-image: url("../public/images/bg-triangle.svg");
  background-repeat: no-repeat;
  background-position: center;
}

.paper, .scissors, .rock {
  cursor: pointer;
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

</style>
