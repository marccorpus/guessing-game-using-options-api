<template>
  <el-row>
    <el-col :span="16" :offset="4">
      <el-card class="card">
        <h3>I am thinking of a number between 1-1000.</h3>
        <h3>Can you guess it?</h3>
        <el-divider><i class="el-icon-star-on"></i></el-divider>

        <el-button v-if="!playing" type="primary" class="btn" @click="startGame"
          >Start Game</el-button
        >

        <template v-else>
          <GuessForm v-if="!winner" @add-guess="addGuess" />

          <Guesses :random-number="randomNumber" :guesses="guesses" />

          <el-button
            v-if="winner"
            type="primary"
            class="btn"
            @click="restartGame"
            >Restart Game</el-button
          >
        </template>
      </el-card>
    </el-col>
  </el-row>
</template>

<script>
import GuessForm from "./GuessForm.vue";
import Guesses from "./Guesses.vue";

export default {
  data() {
    return {
      playing: false,
      winner: false,
      randomNumber: null,
      guesses: [],
    };
  },
  methods: {
    generateRandomNumber() {
      return Math.floor(Math.random() * 1000) + 1;
    },
    startGame() {
      this.playing = true;
      this.randomNumber = this.generateRandomNumber();
    },
    restartGame() {
      this.winner = false;
      this.randomNumber = this.generateRandomNumber();
      this.guesses = [];
    },
    checkWinner(guess) {
      if (this.randomNumber === +guess) {
        this.winner = true;
      }
    },
    addGuess(guess) {
      this.guesses = [
        ...this.guesses,
        {
          id: new Date().toISOString(),
          number: +guess,
          isCorrect: this.randomNumber === +guess,
        },
      ];

      this.checkWinner(guess);
    },
  },
  components: {
    GuessForm,
    Guesses,
  },
};
</script>

<style scoped>
.card {
  border-radius: 5px !important;
}
</style>
