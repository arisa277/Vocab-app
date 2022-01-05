<template>
  <div class="modal">
    <div class="modal-ray" @click="$emit('close')" />
    <div class="modal-content">
      <div class="moda-window">
        <div class="answer-area">
          <h1>Oops...!</h1>
          <p>
            The answer is <span class="answer">"{{ answer }}"</span>
          </p>
          <button class="close" @click="$emit('close')">OK</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["answer"],
  data() {
    return {};
  }
};
</script>

<style scoped>
.modal,
.modal-ray {
  display: flex;
  align-items: center;
  justify-content: center;
  position: fixed;
  z-index: 30;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
}
.modal-content {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  width: 300px;
  height: 200px;
  z-index: 9999;
  margin: 35% auto;
  padding: 20px 30px;
  background-color: #ded2c2;
  border-radius: 5px;
}
.answer-area h1 {
  color: #819582;
}
.answer-area p {
  margin-top: 30px;
  font-size: 18px;
  color: #202020;
}
.answer {
  color: #cb847a;
  font-weight: bold;
  font-size: 24px;
}
.close {
  background: #819582;
  border: none;
  width: 100%;
  padding: 7px;
  cursor: pointer;
  margin-top: 15px;
  font-weight: bold;
  font-size: 18px;
  color: #202020;
}
</style>
