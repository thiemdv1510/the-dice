<template>
  <div class="wrapper-popup" v-bind:class="getClassPopup">
    <div class="rule">
      <h3>Lịch sử quay</h3>
      <div class="row">
        <div class="col-md-1 color" v-for="(item, key) in this.history" :key="key">
            <div v-for="(record, index) in item" :key="index">
              <div v-if="record===0">
                <div class="dice-history-detail-0 "></div>
              </div>
              <div v-else>
                <div class="dice-history-detail-1"></div>
              </div>
            </div>
        </div>

      </div>
      <button v-on:click="confirm" class="btn btn-primary" style="margin-top: 10px">Đóng</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'popup-rule',
  props: {
    isOpenPopup: { type: Boolean, default: false },
    history: {
      type: Array,
      default() {
        return []
      }
    }
  },
  data() {
    return {

    }
  },
  methods: {
    confirm() {
      this.$emit('handleConfirm')
    }
  },
  computed: {
    getClassPopup: function() {
      return {
        'open-popup': this.isOpenPopup
      }
    }
  }
}
</script>

<style>
.color {
  background-color: #979797;
  padding-top: 10px;
  margin-right: 12px;
  padding-right: 29px;
  border-radius: 15px;
}
.dice-history-detail-0 {
  width: 15px;
  height: 15px;
  border: 1px solid white;
  background: white;
  border-radius: 15px;
  margin-bottom: 10px;
}
.dice-history-detail-1 {
  width: 15px;
  height: 15px;
  border: 1px solid black;
  background: black;
  border-radius: 15px;
  margin-bottom: 10px;
}
.wrapper-popup {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0,0,0,0.4);
  opacity: 0;
  visibility: hidden;
  transition: all .3s ease;
  z-index: 9999999;
}
.wrapper-popup.open-popup {
  opacity: 1;
  visibility: visible;
}
.rule {
  width: 350px;
  padding: 20px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) scale(1.2);
  background-color: #fff;
  position: absolute;
  font-family: Arial, Helvetica, sans-serif;
  transition: all .3s ease;
}
.open-popup .rule {
  transform: translate(-50%, -50%) scale(1);
}
/* scale -> class */
.rule h3 {
  margin-bottom: 10px;
}
.rule .confirm {
  cursor: pointer;
  margin-top: 20px;
  padding: 8px 15px;
  border: 2px solid #333;
  background-color: #fff;
  transition: all .3s ease;
}
.rule .confirm:hover {
  color: #fff;
  background-color: #333;
}
/* kết hợp CSS3 với VueJs để xây dựng hiệu ứng - Zoom in - Zoom out */
</style>
