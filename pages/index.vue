<template>
  <div>
      <button @click="shuffleQuestion">shuffle question</button>
    <div>
      {{ questions.indexOf(currentQuestion) + 1 }}.
      {{ currentQuestion.question }}
    </div>
    <div>
      <button @click="preQuestionHandler">previous</button>
      <input type="text" v-model="currentQuestion.userAnswer" @keyup.enter="userAnswerHandler"/><button
        v-on:click="userAnswerHandler"
      >
        answer
      </button>
      <button @click="nextQuestionHandler">next</button>
    </div>
    <div v-if="currentQuestion.showResult">
      <span>{{ currentQuestion.correct ? "true" : "false" }}</span>
      <span v-if="!currentQuestion.correct">{{ currentQuestion.answer }}</span>
    </div>
  </div>
</template>

<script>
import _ from "lodash";
export default {
  name: "IndexPage",
  data: function () {
    return {
      searchKey: "アルファベット読み方",
      imageOriginLink:
        "https://eigodekore.com/wp-content/uploads/2016/11/38026e5b0dcf0e1b9c3a9750d41a891e.jpg",
      questions: [],
      currentQuestion: null,
      alphabet: {
        a: "エイ",
        b: "ビー",
        c: "シー",
        d: "ディー",
        e: "イー",
        f: "エフ",
        g: "ジー",
        h: "エイチ",
        i: "アイ",
        k: "ケイ",
        l: "エル",
        m: "エム",
        n: "エヌ",
        o: "オウ",
        p: "ピー",
        q: "キュー",
        r: "アール",
        s: "エス",
        t: "ティー",
        u: "ユー",
        v: "ヴィ",
        w: "ダブリュ",
        x: "エックス",
        y: "ワイ",
        z: "ズィー",
      },
    };
  },
  created: function () {
    this.questions = this.generateQuestion();
    this.currentQuestion = this.questions[0];
  },
  methods: {
    generateQuestion: function () {
      let _questions = [];
      for (const key in this.alphabet) {
        _questions.push({
          question: key,
          answer: this.alphabet[key],
          userAnswer: null,
          correct: false,
          showResult: false,
        });
      }
      return _questions;
    },
    shuffleQuestion: function () {
      let _questions = this.generateQuestion();
      this.questions = _.shuffle(_questions);
      this.currentQuestion = this.questions[0]
    },
    nextQuestionHandler: function () {
      const currentQuestionIndex = this.questions.indexOf(this.currentQuestion);
      if (currentQuestionIndex <= this.questions.length - 1 - 1) {
        this.currentQuestion = this.questions[currentQuestionIndex + 1];
      }
    },
    preQuestionHandler: function () {
      const currentQuestionIndex = this.questions.indexOf(this.currentQuestion);
      if (currentQuestionIndex > 0) {
        this.currentQuestion = this.questions[currentQuestionIndex - 1];
      }
    },
    userAnswerHandler: function () {
      if (this.currentQuestion.answer === this.currentQuestion.userAnswer) {
        this.currentQuestion.correct = true;
      } else {
        this.currentQuestion.correct = false;
      }

      this.currentQuestion.showResult = true;
    },
  },
};
</script>

<style scoped>
</style>