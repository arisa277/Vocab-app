<template>
  <div class="daypage">
    <div class="box">
      <div class="title">
        <h1>-Day of the week-</h1>
      </div>
      <div v-show="!processing">
        <button class="start-btn" @click="startGame">start</button>
      </div>
      <div v-show="processing">
        <div v-for="(qa, index) in randomQuestions" :key="qa.id">
          <form @submit.prevent="submitAnswer">
            <div class="card" v-show="index === qIndex">
              <span class="qtext">How to say</span>
              <p class="question">"{{ qa.q }}"</p>
              <span class="qtext">in Swedish?</span>
              <input
                class="input"
                type="text"
                v-model="answer"
                autofocus
                ref="input"
                placeholder="Type Here"
                required
              />
              <button class="submit-btn">submit</button>
            </div>
          </form>
        </div>
        <div>
          <AnswerModal answer="hello" />
          <!-- `nej, the answer is "${this.qas[this.qIndex].a}"`) -->
        </div>
        <div v-show="qIndex === qas.length">
          <div class="result">
            <Result :score="score" :numberOfQ="qas.length" />
          </div>
          <button class="restart-btn" @click="restartGame">restart</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Result from "~/components/Result.vue";
import AnswerModal from "~/components/AnswerModal.vue";
export default {
  components: { Result, AnswerModal },
  data() {
    return {
      processing: false,
      answer: "",
      qIndex: 0,
      score: 0,
      qas: [
        {
          q: "Monday",
          a: "måndag"
        },
        {
          q: "Tuesday",
          a: "tisdag"
        },
        {
          q: "Wednesday",
          a: "onsdag"
        },
        {
          q: "Thursday",
          a: "torsdag"
        },
        {
          q: "Friday",
          a: "fredag"
        },
        {
          q: "Saturday",
          a: "lördag"
        },
        {
          q: "Sunday",
          a: "söndag"
        }
      ]
    };
  },
  computed: {
    randomQuestions() {
      return this.qas.sort(() => 0.5 - Math.random());
    }
  },
  mounted() {
    // setTimeout(() => {
    //    this.$refs.input[0].focus();
    // }, 1000)
  },
  methods: {
    submitAnswer() {
      if (this.qas[this.qIndex].a === this.answer) {
        this.score++;
      } else {
        this.show();
      }
      this.answer = "";
      this.qIndex++;
    },
    startGame() {
      this.processing = true;
    },
    restartGame() {
      this.qIndex = 0;
    },
    show() {
      this.$modal.show("modal-content");
    },
    hide() {
      this.$modal.hide("modal-content");
    }
  }
};
</script>

<style scoped>
.title h1 {
  color: #c2c9c9;
  margin-bottom: 50px;
  font-family: "Courier New";
}
.daypage {
  height: 100vh;
  text-align: center;
  background: #819582;
  display: flex;
  justify-content: center;
  align-items: center;
}
.question {
  font-family: "Courier New";
  color: #cb847a;
  font-size: 30px;
  font-weight: bold;
}
.input {
  margin: 10px 0;
  outline: none;
  border: none;
  width: 100%;
  height: 30px;
  font-size: 100%;
  text-align: center;
}
.start-btn {
  background: #ded2c2;
  border: none;
  width: 100%;
  padding: 7px;
  cursor: pointer;
  font-weight: bold;
  font-size: 18px;
}
.submit-btn {
  background: #ded2c2;
  border: none;
  width: 100%;
  padding: 7px;
  cursor: pointer;
  font-weight: bold;
  font-size: 18px;
  color: #202020;
}
.restart-btn {
  background: #ded2c2;
  border: none;
  width: 100%;
  padding: 7px;
  cursor: pointer;
  font-weight: bold;
  color: #202020;
}
.qtext {
  font-size: 18px;
  color: #c2c9c9;
}
/* Modal */
.modal-content {
}
</style>
