<template>
  <div id="app">
    <audio controls autoplay loop>
      <source src="../src/assets/audio/KiepDoDen-DuyManh_bbt.mp3" type="audio/mpeg">
    </audio>
    <div class="wrapper clearfix table-background">
      <players
          :winnerIsTai="winnerIsTai"
          :winnerIsXiu="winnerIsXiu"
          @handleBetTai="handleBetTai"
          @handleBetXiu="handleBetXiu"
          :betTai="showTotalMoneyBetTai"
          :betXiu="showTotalMoneyBetXiu"
      />

      <controls
          v-bind:finalScore="showMoneyResult"
          v-on:handleChangeFinalScore="handleChangeFinalScore"
          v-on:handleRollDice="handleRollDice"
          :diceHistory="diceHistory"
          @showPopup="showPopup"
          @betResult="betResult"
          @handlePlus="handlePlus"
          :totalMoneyBet="totalMoneyBet"
      />

      <dices
          v-bind:dices="dices"
      />
      <popup-rule :isOpenPopup="isOpenPopup" :history="dataPopup" @handleConfirm="handleConfirm"/>
    </div>
  </div>
</template>

<script>
import Controls from './components/Controls';
import Dices from './components/Dices';
import Players from "./components/Players";
import PopupRule from './components/PopupRole';

export default {
  name: 'app',
  data () {
    return {
      dices: [2, 6, 1],
      currentScore: 0,
      diceHistory: [],
      showDiceHistory: [],
      winnerIsTai: false,
      winnerIsXiu: false,
      isOpenPopup: false,
      isBetTai: true,
      showTotalMoneyBetTai: 0,
      showTotalMoneyBetXiu: 0,
      hideTotalMoneyBetTai: 0,
      hideTotalMoneyBetXiu: 0,
      totalBet: {
        type: '',
        money: 0,
      },
      countRoll: 0,
      moneyResult: 10000,
      showMoneyResult: 0,
      totalMoneyBet: 0,
      dataPopup: [],
    }
  },
  components: {
    Controls,
    Dices,
    Players,
    PopupRule,
  },
  computed: {

  },
  created() {
    this.showMoneyResult = this.moneyResult.toLocaleString()
  },
  watch: {
    moneyResult: function() {
      this.showMoneyResult = this.moneyResult.toLocaleString()
    }
  },
  methods: {
    handlePlus(total) {
      if ((total + this.hideTotalMoneyBetTai + this.hideTotalMoneyBetXiu) > this.moneyResult) {
        alert('Số tiền đặt cược không đủ !')
        this.totalMoneyBet = 0
        return false
      }
      this.totalMoneyBet += total
      if (this.isBetTai) {
        this.showTotalMoneyBetTai = this.totalMoneyBet.toLocaleString()
        this.hideTotalMoneyBetTai = this.totalMoneyBet
      } else {
        this.hideTotalMoneyBetXiu = this.totalMoneyBet
        this.showTotalMoneyBetXiu = this.totalMoneyBet.toLocaleString()
      }
    },
    betResult() {
      this.totalBet.type = this.isBetTai
      this.totalBet.money = this.hideTotalMoneyBetTai + this.hideTotalMoneyBetXiu
      this.moneyResult -= this.totalBet.money
    },
    handleBetTai() {
      this.showTotalMoneyBetXiu = 0
      this.showTotalMoneyBetTai = 0
      this.hideTotalMoneyBetTai = 0
      this.hideTotalMoneyBetXiu = 0
      this.totalMoneyBet = 0
      this.isBetTai = true
    },
    handleBetXiu() {
      this.showTotalMoneyBetXiu = 0
      this.showTotalMoneyBetTai = 0
      this.hideTotalMoneyBetTai = 0
      this.hideTotalMoneyBetXiu = 0
      this.totalMoneyBet = 0
      this.isBetTai = false
    },
    handleConfirm() {
      this.isOpenPopup = false
    },
    showPopup() {
      const countPage = Math.ceil(this.diceHistory.length/10)
      let arr = []

      for (let i = 1; i <= countPage; i++) {
        const from = (i - 1)*10
        arr[i] = this.diceHistory.slice(from, from + 10)
      }
      this.dataPopup = arr
      this.isOpenPopup = true
    },
    handleRollDice() {
      const dice1 = Math.floor(Math.random() * 6) + 1;
      const dice2 = Math.floor(Math.random() * 6) + 1;
      const dice3 = Math.floor(Math.random() * 6) + 1;
      this.dices = [dice1, dice2, dice3];
      const total = dice1 + dice2 + dice3
      if (total > 10) {
        this.winnerIsTai = true
        this.winnerIsXiu = false
        this.diceHistory.push(1)
        if (this.totalBet.type) {
          this.moneyResult += this.totalBet.money * 2
        }
      } else {
        if (!this.totalBet.type) {
          this.moneyResult += this.totalBet.money * 2
        }
        this.winnerIsTai = false
        this.winnerIsXiu = true
        this.diceHistory.push(0)
      }
      const length = this.diceHistory.length
      if (length > 24) {
        this.diceHistory =  [...this.diceHistory.slice(length - 1, length)]
      }
    },
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;

}
.table-background {
  background-image: url("./assets/table-1.jpg");
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
}
.player-panel {
  width: 50%;
  float: left;
  height: 600px;
  padding: 100px;
  transition: all .3s ease;
}

.clearfix::after {
  content: "";
  display: table;
  clear: both;
}

body {
  background-image: linear-gradient(rgba(62, 20, 20, 0.4), rgba(62, 20, 20, 0.4)), url('./assets/back.jpg');
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
  box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
  overflow: hidden;
  border-radius: 15px;
}
</style>
