<template>
  <div id="app">
    <div class="wrapper clearfix">
      <players v-bind:scorePlayer="scorePlayer" v-bind:activePlayer="activePlayer" />
      <controls v-on:handleNewGame="handleNewGame" v-on:handleRollDice="handleRollDice" />
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
      dice: [5, 6]
    };
  },
  created() {},
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
        let dice1 = parseInt(Math.random() * 6);
        let dice2 = parseInt(Math.random() * 6);
        this.dice = [dice1, dice2];
      }
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
