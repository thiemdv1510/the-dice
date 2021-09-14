<template>
  <div class="">
    <!-- Danh sach Product -> ProductItem -->
    <div class="player-panel rangoliPic" >
      <div class="text-tai" v-if="!winnerIsTai">Tài</div>
      <div class="player-name-tai" v-else>
        <!--              <video class="video-tai" poster="//i.imgur.com/FibOoe5h.jpg" preload="auto" autoplay="autoplay" muted="muted" loop="loop" style="width: 222px; height: 222px;">
                        <source src="//i.imgur.com/FibOoe5.mp4" type="video/mp4">
                      </video>-->
        <img src="../assets/tai-music.gif" alt="">
      </div>
      <div class="row">
        <div class="col-md-8">
          <input readonly class="form-control input-bet" type="text" :value="betTai">
        </div>
        <div class="col-md-4">
          <button @click="clickBetTai" class="btn btn-primary cuoc-tai">Đặt</button>
        </div>
      </div>

    </div>

    <div class="player-panel" :class="winnerIsXiu">
      <div class="text-xiu" v-if="!winnerIsXiu">Xỉu</div>
      <div class="player-name-xiu" v-else>
        <!--            <video class="video-xiu" poster="//i.imgur.com/FibOoe5h.jpg" preload="auto" autoplay="autoplay" muted="muted" loop="loop" style="width: 222px; height: 222px;">
                      <source src="//i.imgur.com/FibOoe5.mp4" type="video/mp4">
                    </video>-->
        <img src="../assets/xiu-resized.gif" alt="">
      </div>
      <div class="row">
        <div class="col-md-8">
          <input readonly class="form-control input-bet ml-6" type="text" :value="betXiu" >
        </div>
        <div class="col-md-4">
          <button @click="clickBetXiu" class="btn btn-primary cuoc-xiu">Đặt</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'players',
  props: {
    winnerIsTai: { type: Boolean, default: false },
    winnerIsXiu: { type: Boolean, default: false },
    betTai: String,
    betXiu: String,
  },
  data() {
    return {
    }
  },
  methods: {
    clickBetTai() {
      this.$emit('handleBetTai')
    },
    clickBetXiu() {
      this.$emit('handleBetXiu')
    }
  }
}
</script>

<style>
.cuoc-xiu{
  top: 47%;
  right: 10%;
  position: absolute;
  height: 34px;
  font-size: 13px;
  font-family: 'Ionicons';
}
.cuoc-tai {
  font-size: 13px;
  font-family: 'Ionicons';
  position: absolute;
  top: 47%;
  right: 68%;
}
.input-bet {
  position: absolute;
  top: 47%;
  width: 145px;
  height: 35px;
}
.ml-6 {
  margin-left: 84px;
}
.text-tai {
  position: absolute;
  top: 25%;
  right: 80%;
  transform: translate(50%,-50%);
  text-transform: uppercase;
  font-family: verdana;
  font-size: 6em;
  font-weight: 700;
  color: #2d2c2b;
  text-shadow: 1px 1px 1px #919191,
  1px 2px 1px #ffffff,
  1px 3px 1px #ffffff,
  1px 4px 1px #ffffff,
  1px 5px 1px #ffffff,
  1px 6px 1px #ffffff,
  1px 7px 1px #ffffff,
  1px 8px 1px #ffffff,
  1px 9px 1px #ffffff,
  1px 10px 1px #ffffff,
  1px 18px 6px rgba(16,16,16,0.4),
  1px 22px 10px rgba(16,16,16,0.2),
  1px 25px 35px rgba(16,16,16,0.2),
  1px 30px 60px rgba(16,16,16,0.4);
}
.text-xiu {
  position: absolute;
  top: 25%;
  right: 21%;
  transform: translate(50%,-50%);
  text-transform: uppercase;
  font-family: verdana;
  font-size: 6em;
  font-weight: 700;
  color: #ffffff;
  text-shadow: 1px 1px 1px #919191, 1px 2px 1px #919191, 1px 3px 1px #919191, 1px 4px 1px #919191, 1px 5px 1px #919191, 1px 6px 1px #919191, 1px 7px 1px #919191, 1px 8px 1px #919191, 1px 9px 1px #919191, 1px 10px 1px #919191, 1px 18px 6px rgb(16 16 16 / 40%), 1px 22px 10px rgb(16 16 16 / 20%), 1px 25px 35px rgb(16 16 16 / 20%), 1px 30px 60px rgb(16 16 16 / 40%);
}
.video-xiu {
  top: -46%;
  position: absolute;
  right: 15%;
  opacity: 50%;
  border-radius: 15px;
}
.video-tai {
  top: -46%;
  position: absolute;
  opacity: 58%;
  right: 15%;
  border-radius: 13px;
}
.player-panel {
  width: 50%;
  float: left;
  height: 600px;
  padding: 100px;
  transition: all .3s ease;
}
.player-name-xiu {
  font-family: 'Ionicons';
  font-size: 100px;
  text-align: center;
  text-transform: uppercase;
  letter-spacing: 2px;
  font-weight: 100;
  margin-top: 20px;
  margin-bottom: 10px;
  position: relative;
  z-index: 999;
  color: black;
  right: -7%;
  top: -17%;
  border-radius: 15px;
}
.player-name-tai {
  font-family: 'Ionicons';
  font-size: 100px;
  text-align: center;
  text-transform: uppercase;
  letter-spacing: 2px;
  font-weight: 100;
  margin-top: 20px;
  margin-bottom: 10px;
  position: relative;
  z-index: 999;
  color: black;
  right: 27%;
  top: -23%;
  border-radius: 15px;
}
.rangoliPic {
  background-image: url('https://i.imgur.com/FibOoe5.gifv') !important
}


</style>
