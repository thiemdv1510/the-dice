<template>
  <div class="">
    <button
        v-on:click="rollDice"
        class="control btn-roll"><i class="ion-ios-loop"></i>Roll dice</button>
    <input
        v-bind:disabled="isPlaying"
        v-bind:value="finalScore"
        type="text" placeholder="Final score" class="final-score">
    <div class="dice-history">
      <div v-for="(item,key) in diceHistory" :key="key" >
        <div v-if="item===0"  class="dice-history-detail-0"></div>
        <div v-else class="dice-history-detail-1"></div>
      </div>

    </div>
    <a href="javascript:void(0)" title="Hiển thị lịch sử">
      <ion-icon @click="showPopup" name="eye-outline" class="btn-show-detail-history"></ion-icon>
    </a>
    <div class="list-btn-bet">
      <a href="javascript:void(0)" @click="handlePlus(1000)" class="myButton mr-7">1k</a>
      <a href="javascript:void(0)" @click="handlePlus(10000)" class="myButton mr-7">10k</a>
      <a href="javascript:void(0)" @click="handlePlus(50000)" class="myButton mr-7">50K</a>
      <a href="javascript:void(0)" @click="handlePlus(100000)" class="myButton mr-7">100K</a>
      <a href="javascript:void(0)" @click="handlePlus(1000000)" class="myButton mr-7">1M</a>
      <a href="javascript:void(0)" @click="handlePlus(10000000)" class="myButton mr-7">10M</a>
      <a href="javascript:void(0)" @click="handlePlus(50000000)" class="myButton mr-7">50M</a>
      <button @click="betResult" class="btn btn-primary" style="height: 47px;">Cược</button>
    </div>

  </div>
</template>

<script>
export default {
  name: 'controls',
  props: {
    finalScore: {
      type: String,
      default() {
        return 100
      }},
    isPlaying: { type: Boolean, default: false },
    diceHistory: {
      type: Array,
      default() {
        return [1, 1, 1, 0]
      }
    }
  },
  data() {
    return {
      valueDemo: 100,
      classDiceTai: 'dice-history-detail-1',
      classDiceXiu: 'dice-history-detail-0',
    }
  },
  methods: {
    handlePlus(money) {
      this.$emit('handlePlus', money);
    },
    betResult() {
      this.$emit('betResult', this.totalMoneyBet);
    },
    showPopup() {
      this.$emit('showPopup');
    },
    rollDice() {
      this.$emit('handleRollDice');
    }
  }
}
</script>

<style>
.myButton {
  text-align: center;
  background-color: #44c767;
  border-radius: 24px;
  border: 1px solid #18ab29;
  display: inline-block;
  cursor: pointer;
  color: #ffffff;
  font-family: 'Ionicons';
  font-size: 17px;
  padding: 10px 18px;
  text-decoration: none;
  text-shadow: 0 1px 0 #2f6627;
}
.myButton:hover {
  background-color:#5cbf2a;
}
.myButton:active {
  position:relative;
  top:1px;
}

.mr-20 {
  margin-right: 20px;
}
.mr-7 {
  width: 71px;
  margin-right: 7px;
}
.list-btn-bet {
  position: absolute;
  top: 70%;
  right: 21%;
}
.btn-show-detail-history {
  position: absolute;
  top: 61%;
  right: 20%;
  color: #0f3e6f;
}
.dice-history-detail-0 {
  width: 15px;
  height: 15px;
  border: 1px solid white;
  background: white;
  border-radius: 15px;
  margin-right: 5px;
}
.dice-history-detail-1 {
  width: 15px;
  height: 15px;
  border: 1px solid black;
  background: black;
  border-radius: 15px;
  margin-right: 5px;
}
.dice-history {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  top: 60%;
  text-align: center;
  padding: 10px;
  text-transform: uppercase;
  width: 532px;
  border: 1px solid;
  border-radius: 15px;
  height: 35px;
  background-color: #ccc;
  display: inline-flex;
}
.control {
  position: absolute;
  width: 200px;
  left: 50%;
  transform: translateX(-50%);
  color: #555;
  background: none;
  border: none;
  font-family: Lato;
  font-size: 20px;
  text-transform: uppercase;
  cursor: pointer;
  font-weight: 300;
  transition: background-color 0.3s, color 0.3s;
}
.control.disable {
  pointer-events: none;
}

.control:hover { font-weight: 600; }
.control:hover i { margin-right: 20px; }

.control:focus {
  outline: none;
}

.control i {
  color: #42b983;
  display: inline-block;
  margin-right: 15px;
  font-size: 32px;
  line-height: 1;
  vertical-align: text-top;
  margin-top: -4px;
  transition: margin 0.3s;
}

.btn-new { top: 45px;}
.btn-roll {
  top: 10%;
  color: ivory;
  font-family: 'Ionicons'
}
.btn-hold { top: 467px;}

.final-score {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  top: 520px;
  color: #555;
  font-size: 18px;
  font-family: 'Lato';
  text-align: center;
  padding: 10px;
  width: 160px;
  text-transform: uppercase;
}

.final-score:focus { outline: none; }
</style>
