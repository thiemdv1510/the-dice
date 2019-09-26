<template>
  <div id="app">
    <div class="wrapper clearfix">
      <players
        v-bind:scorePlayer="scorePlayer"
        v-bind:activePlayer="activePlayer"
        v-bind:currentScore="currentScore"
        v-bind:playerWinner="playerWinner"
        v-bind:isWinner="isWinner"
      />
      <controls
        v-on:handleNewGame="handleNewGame"
        v-on:handleRollDice="handleRollDice"
        v-on:handleHold="handleHold"
        v-on:changeFinalScore="changeFinalScore"
        v-bind:activeGame="activeGame"
        v-bind:finalScore="finalScore"
      />
      <dices v-bind:dice="dice" />
      <popup-role v-bind:showPopupRole="showPopupRole" v-on:handleAgree="handleAgree" />
    </div>
  </div>
</template>

<script>
import Players from "./components/Players";
import Controls from "./components/Controls";
import Dices from "./components/Dices";
import PopupRole from "./components/PopupRole";

export default {
  name: "app",
  data() {
    return {
      showPopupRole: false,
      activeGame: false,
      activePlayer: 1,
      scorePlayer: [6, 9],
      currentScore: 0,
      dice: [5, 6],
      finalScore: 0,
      playerWinner: 0
    };
  },
  created() {},
  computed: {
    isWinner() {
      if (
        this.scorePlayer[0] >= this.finalScore ||
        this.scorePlayer[1] >= this.finalScore
      ) {
        this.activeGame = false;
        return true;
      } else {
        return false;
      }
    }
  },
  methods: {
    handleNewGame() {
      console.log("HandleNewGame");
      this.showPopupRole = true;
    },
    handleAgree() {
      console.log("HandleAgree");
      this.activeGame = true;
      this.scorePlayer = [0, 0];
      this.currentScore = 0;
      this.activePlayer = 0;
      this.showPopupRole = false;
    },
    handleRollDice() {
      if (this.activeGame) {
        // let dice1 = Math.floor(Math.random() * 6);
        // let dice2 = Math.floor(Math.random() * 6);
        this.dice = [this.randomNumberLowerSix(), this.randomNumberLowerSix()];
        this.currentScore = this.dice.reduce((accumulator, currentValue) => {
          return accumulator + currentValue;
        });
      } else {
        alert("Please press new game button!!!");
      }
    },
    handleHold() {
      console.log("handle hold");
      if (this.activeGame) {
        this.updateScorePlayer();
        if (!this.isWinner) {
          this.activePlayer = this.activePlayer == 0 ? 1 : 0;
          this.currentScore = 0;
        }
      } else {
        alert("Please press new game button!!!");
      }
    },
    updateScorePlayer() {
      if (this.activePlayer == 0) {
        this.scorePlayer = [
          this.scorePlayer[0] + this.currentScore,
          this.scorePlayer[1]
        ];
      } else {
        this.scorePlayer = [
          this.scorePlayer[0],
          this.scorePlayer[1] + this.currentScore
        ];
      }
    },
    changeFinalScore(e) {
      console.log("final score");
      let finalScore = parseInt(e.target.value);
      console.log(finalScore);
      if (isNaN(finalScore)) {
        this.finalScore = 0;
      } else {
        this.finalScore = finalScore;
      }
    },
    randomNumberLowerSix() {
      return Math.floor(Math.random() * 6);
    }
  },
  components: {
    Players,
    Controls,
    Dices,
    PopupRole
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.clearfix::after {
  content: "";
  display: table;
  clear: both;
}

body {
  background-image: linear-gradient(
      rgba(62, 20, 20, 0.4),
      rgba(62, 20, 20, 0.4)
    ),
    url("assets/back.jpg");
  background-size: cover;
  background-position: center;
  font-family: Lato;
  font-weight: 300;
  position: relative;
  height: 100vh;
  color: #555;
}

.wrapper {
  width: 1000px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #fff;
  box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
  overflow: hidden;
}
</style>
