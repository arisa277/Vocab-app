<template>
  <div class="box">
    <div class="title">
      <h1>-Tidsattack-</h1>
    </div>
    <div v-show="!processing && !isFinished">
      <button class="start-btn" @click="startGame">Start</button>
      <!-- <p class="back_btn"><nuxt-link to="/">back</nuxt-link></p> -->
    </div>
    <div v-show="processing && !isFinished">
      <p class="timer" :style="{ color: timeLimit ? 'red' : 'white' }">
        {{ timerNumber }}
      </p>
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
            <button class="submit-btn">Submit</button>
          </div>
        </form>
      </div>
    </div>
    <div>
      <div v-show="!processing && isFinished">
        <p class="score">Your score is {{ score }} outof {{ qas.length }}</p>
        <div class="messages">
          <p v-if="score === 0">Nej...</p>
          <p v-else-if="score / qas.length <= 0.3">Bra!</p>
          <p v-else-if="0.4 <= score / qas.length <= 0.7">Jättebra!</p>
          <p v-else>Fantastiskt!</p>
        </div>
        <p class="review">Let's review these vocabs!</p>
        <div class="result" v-for="wa in wrongAnswers" :key="wa.id">
          <p>❌ {{ wa.w }}</p>
          <p class="correctAnswer">⭕️ {{ wa.a }}</p>
        </div>
        <button class="restart-btn" @click.prevent="restartGame">
          Restart
        </button>
      </div>
    </div>
    <p class="back_btn" @click="finish"><nuxt-link to="/">Home</nuxt-link></p>
  </div>
</template>

<style scoped>
.score {
  margin: 5px 0;
  font-size: 18px;
  color: #da8074;
}
.messages {
  margin-bottom: 5px;
  color: #da8074;
  font-weight: bold;
  font-size: 30px;
}
.result {
  background: whitesmoke;
  padding: 10px;
  margin-bottom: 10px;
  color: #202020;
  display: flex;
  justify-content: space-between;
}
.timer {
  font-size: 20px;
  margin-bottom: 20px;
  font-weight: bold;
}
.correctAnswer {
  color: #da8074;
  font-weight: bold;
}
.review {
  color: rgba(0, 0, 0, 0.7);
  margin: 10px 0;
  font-weight: bold;
}
</style>

<script>
export default {
  data() {
    return {
      processing: false,
      answer: "",
      qIndex: 0,
      score: 0,
      wrongAnswers: [],
      timerEnabled: true,
      timerNumber: "30:00",
      start: new Date(),
      countDown: "",
      isFinished: false,
      timeLimit: false,
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
        },
        {
          q: "January",
          a: "januari"
        },
        {
          q: "February",
          a: "februari"
        },
        {
          q: "March",
          a: "mars"
        },
        {
          q: "April",
          a: "april"
        },
        {
          q: "May",
          a: "maj"
        },
        {
          q: "June",
          a: "juni"
        },
        {
          q: "July",
          a: "juli"
        },
        {
          q: "August",
          a: "augusti"
        },
        {
          q: "September",
          a: "september"
        },
        {
          q: "October",
          a: "oktober"
        },
        {
          q: "November",
          a: "november"
        },
        {
          q: "December",
          a: "december"
        }
      ]
    };
  },
  computed: {
    randomQuestions() {
      return this.qas.sort(() => 0.5 - Math.random());
    }
  },
  methods: {
    startGame() {
      this.start = new Date();
      this.processing = true;
      this.countDown = setInterval(() => {
        this.timer();
      }, 10);
      this.$nextTick(() => {
        this.$refs.input[this.qIndex].focus();
      });
    },
    submitAnswer() {
      if (this.qas[this.qIndex].a === this.answer.trim().toLowerCase()) {
        this.score++;
        this.qIndex++;
      } else {
        this.wrongAnswers.push({ a: this.qas[this.qIndex].a, w: this.answer });
        this.qIndex++;
      }
      if (this.qIndex === this.$refs.input.length) {
        return;
      } else {
        this.$nextTick(() => {
          this.$refs.input[this.qIndex].focus();
        });
      }
      this.answer = "";
    },
    restartGame() {
      this.start = new Date();
      this.timerNumber = "30:00";
      this.score = 0;
      this.qIndex = 0;
      this.isFinished = false;
      this.processing = true;
      this.answer = "";
      (this.wrongAnswers = []),
        (this.countDown = setInterval(() => {
          this.timer();
        }, 10));
      this.$nextTick(() => {
        this.$refs.input[this.qIndex].focus();
      });
    },
    timer() {
      let point = "";
      let sec = "";
      let seconds = "";
      let min = "";
      let hour = "";
      let now = "";
      let time = "";

      now = new Date();
      time = now.getTime() - this.start.getTime();

      point = Math.floor(time / 100);
      sec = Math.floor(time / 1000);
      min = Math.floor(sec / 60);
      hour = Math.floor(min / 60);
      seconds = Math.floor(time / 1000);

      if (seconds < 20) {
        point = 9 - (point - sec * 10);
        sec = 30 - (sec - min * 60);
        min = 0 - (min - hour * 60);

        point = this.addZero(point);
        sec = this.addZero(sec);
        min = this.addZero(min);
        this.timerNumber = min + ":" + sec + ":" + point;
      } else if (20 <= seconds && seconds < 30) {
        point = 9 - (point - sec * 10);
        sec = 30 - (sec - min * 60);
        min = 0 - (min - hour * 60);

        point = this.addZero(point);
        sec = this.addZero(sec);
        min = this.addZero(min);
        this.timeLimit = true;
        this.timerNumber = min + ":" + sec + ":" + point;
      } else {
        clearInterval(this.countDown);
        this.timerNumber = "00:00:00";
        this.isFinished = true;
        this.processing = false;
        this.counter = "";
        this.timeLimit = false;
        this.confettiStart();
        setTimeout(() => {
          this.confettiStop();
        }, 2000);
        console.log("Finished counter");
        this.start = new Date();
      }
    },
    finish() {
      clearInterval(this.countDown);
      this.timerNumber = "00:00:00";
      this.isFinished = true;
      this.processing = false;
      this.counter = "";
      this.timeLimit = false;
      this.start = new Date();
    },
    addZero(value) {
      if (value < 10) {
        value = "0" + value;
      }
      return value;
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
