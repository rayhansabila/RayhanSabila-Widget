<template>
  <div class="guess-number-game">
    <h2>Tebak Angka</h2>
    <p v-if="!gameOver">Tebak angka antara 1 dan 100:</p>
    <p v-if="gameOver">Permainan selesai. Angka yang benar adalah {{ randomNumber }}</p>
    <input type="number" v-model="guess" v-bind:disabled="gameOver" />
    <button v-bind:disabled="gameOver" @click="checkGuess">Tebak</button>
    <p v-if="resultMessage">{{ resultMessage }}</p>
    <button @click="resetGame">Mulai Ulang</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      guess: null,
      randomNumber: null,
      resultMessage: '',
      gameOver: false
    };
  },
  methods: {
    startGame() {
      this.randomNumber = Math.floor(Math.random() * 100) + 1;
    },
    checkGuess() {
      if (this.guess === this.randomNumber) {
        this.resultMessage = 'Selamat! Angka yang Anda tebak benar!';
        this.gameOver = true;
      } else if (this.guess < this.randomNumber) {
        this.resultMessage = 'Angka terlalu rendah. Coba lagi!';
      } else {
        this.resultMessage = 'Angka terlalu tinggi. Coba lagi!';
      }
    },
    resetGame() {
      this.guess = null;
      this.randomNumber = null;
      this.resultMessage = '';
      this.gameOver = false;
      this.startGame();
    }
  },
  mounted() {
    this.startGame();
  }
};
</script>

<style>

body{
  background-color: #E8D2A6;
}

.guess-number-game {
  text-align: center;
  padding: 20px;
}

button {
  margin-top: 10px;
  padding: 8px 16px;
  border: none;
  background-color: #333;
  color: #fff;
  font-size: 16px;
  font-weight: bold;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #555;
}
</style>
