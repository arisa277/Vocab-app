<template>
  <div class="box">
    <div class="title">
      <h1>-{{ title }}-</h1>
    </div>
    <div v-show="!processing">
      <button class="start-btn" @click="startGame">Start</button>
    </div>
    <div v-show="processing">
      <div v-for="(qa, index) in randomQuestions" :key="qa.id">
        <form @submit.prevent="submitAnswer" v-if="!correctProcessing">
          <div class="card" v-show="index === qIndex">
            <span class="qtext">How to say</span>
            <p class="question">"{{ qa.q }}"</p>
            <span class="qtext">in Swedish?</span>
            <input
              class="input"
              type="text"
              v-model="answer"
              ref="input"
              placeholder="Type Here"
              required
            />
            <button class="submit-btn">Submit</button>
          </div>
        </form>
      </div>
      <p v-if="correctProcessing">Congrats! 🎉🎉🎉</p>
      <div v-if="wrong">
        <AnswerModal :answer="qas[qIndex].a" @close="closeModal" />
      </div>
      <div v-show="qIndex === qas.length">
        <div class="result">
          <Result :score="score" :numberOfQ="qas.length" />
        </div>
        <button class="restart-btn" @click="restartGame">Restart</button>
      </div>
    </div>
    <p class="back_btn" @click="finish"><nuxt-link to="/">Home</nuxt-link></p>
  </div>
</template>

<script>
import Result from "~/components/Result.vue";
import AnswerModal from "~/components/AnswerModal.vue";
export default {
  props: ["qas", "title"],
  components: { Result, AnswerModal },
  data() {
    return {
      processing: false,
      correctProcessing: false,
      answer: "",
      qIndex: 0,
      score: 0,
      wrong: false
    };
  },
  computed: {
    randomQuestions() {
      return this.qas.sort(() => 0.5 - Math.random());
    }
  },
  methods: {
    submitAnswer() {
      // if the answer is correct
      if (this.qas[this.qIndex].a === this.answer.trim().toLowerCase()) {
        this.correctProcessing = true;
        this.confettiStart();
        setTimeout(() => {
          this.confettiStop();
        }, 500);
        setTimeout(() => {
          this.score++;
          this.qIndex++;
          this.correctProcessing = false;
          if (this.qIndex === this.$refs.input.length) {
            return;
          } else {
            this.$nextTick(() => {
              this.$refs.input[this.qIndex].focus();
            });
          }
        }, 1000);
        // if the answer is not correct
      } else {
        this.wrong = true;
      }
      this.answer = "";
    },
    startGame() {
      this.processing = true;
      this.$nextTick(() => {
        this.$refs.input[this.qIndex].focus();
      });
    },
    restartGame() {
      this.score = 0;
      this.qIndex = 0;
      this.processing = false;
    },
    closeModal() {
      this.qIndex++;
      this.wrong = false;
      if (this.qIndex === this.$refs.input.length) {
        return;
      } else {
        this.$nextTick(() => {
          this.$refs.input[this.qIndex].focus();
        });
      }
    },
    finish() {
      this.score = 0;
      this.qIndex = 0;
    },
    confettiStart() {
      this.$confetti.start();
    },
    confettiStop() {
      this.$confetti.stop();
    }
  }
};
</script>
