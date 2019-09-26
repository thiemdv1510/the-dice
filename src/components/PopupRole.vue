<template>
  <div class="wrap-popup-role" v-bind:class="{active:showPopupRole}">
    <div class="role">
      <h3>Role Game</h3>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Officia, consectetur explicabo. Quidem omnis vero fugiat amet aliquid ad quos distinctio expedita quis autem recusandae illum earum, corrupti consequuntur consequatur provident?</p>
      <button @click="agree">Yes, I was read</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "popup-role",
  props: {
    showPopupRole: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {};
  },
  methods: {
    agree() {
      this.$emit("handleAgree");
    }
  }
};
</script>

<style>
.wrap-popup-role {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  top: 0;
  background: rgba(0, 0, 0, 0.4);
  opacity: 0;
  visibility: hidden;
  transition: all 0.3s ease-in;
}
.wrap-popup-role.active {
  opacity: 1;
  visibility: visible;
  transition: all 0.3s ease-in;
}
.role {
  background: white;
  position: absolute;
  top: 50%;
  left: 50%;
  width: 300px;
  transform: translate(-50%, -50%) scale(1.2);
  transition: all 0.3s ease;
  padding: 20px;
}
.active .role {
  transform: translate(-50%, -50%) scale(1);
  transition: all 0.3s ease;
}
.role p {
  margin: 10px 0px;
}

.role button {
  padding: 10px 8px;
  background: white;
  border: 2px solid black;
  border-radius: 5px;
  transition: all 0.3s ease;
}

.role button:hover {
  background: black;
  border: 2px solid white;
  color: white;
  transition: all 0.3s ease;
}
</style>