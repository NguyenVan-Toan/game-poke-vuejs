<template>
  <div class="mainScreen">
    <main-screen
      v-if="statusDisplay === 'mainScreen'"
      @SelectModeGame="handleSelectModeGame($event)"
    />
  </div>
  <game-screen
    v-if="statusDisplay === 'gameScreen'"
    @BackToMain="handleBackToMain"
    :cardContext="settings.cardContext"
    @EndGame="handleEndGame"
  />
  <end-game-screen
    v-if="statusDisplay === 'endGameScreen'"
    :timer="timer"
    @onStartAgain="handleBackToMain"
  />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import GameScreen from "./components/GameScreen.vue";
import { shuffled } from "./utils/arrayMix.js";
import EndGameScreen from "./components/EndGameScreen.vue";

export default {
  name: "App",
  components: {
    MainScreen,
    GameScreen,
    EndGameScreen,
  },
  data() {
    return {
      statusDisplay: "mainScreen",
      settings: {
        totalOfBlocks: 0,
        cardContext: [],
        startAt: null,
      },
      timer: 0,
    };
  },
  methods: {
    handleSelectModeGame(config) {
      this.settings.totalOfBlocks = config.totalOfBlocks;
      const firstArray = Array.from(
        { length: this.settings.totalOfBlocks / 2 },
        (_, i) => i + 1
      );
      const secondArray = [...firstArray];
      const cards = firstArray.concat(secondArray);
      this.settings.cardContext = shuffled(shuffled(cards));
      this.settings.startAt = new Date().getTime();
      this.statusDisplay = "gameScreen";
    },
    handleBackToMain() {
      this.statusDisplay = "mainScreen";
    },
    handleEndGame() {
      const timeEnd = new Date().getTime();
      this.timer = timeEnd - this.settings.startAt;
      setTimeout(() => {
        this.statusDisplay = "endGameScreen";
      }, 900);
    },
  },
};
</script>

<style>
#app {
  /* -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50; */
}
</style>
