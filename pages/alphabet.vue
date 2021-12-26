<template>
  <div>
    <div>
      {{ currentQuestionIndex + 1 }}.
      {{ questions[currentQuestionIndex].question }}
    </div>
    <div><input type="text" /></div>
  </div>
</template>

<script>
import _ from "lodash";
export default {
  data: {
    searchKey: "アルファベット読み方",
    imageOriginLink:
      "https://eigodekore.com/wp-content/uploads/2016/11/38026e5b0dcf0e1b9c3a9750d41a891e.jpg",
    questions: [],
    currentQuestionIndex: 0,
    alphabet: {
      a: "",
      b: "",
      c: "",
      d: "",
      e: "",
      f: "",
      g: "",
      h: "",
      i: "",
      k: "",
      l: "",
      m: "",
      n: "",
      o: "",
      p: "",
      t: "",
      u: "",
      v: "",
      w: "",
      x: "",
      y: "",
      z: "",
    },
  },
  created: function(){
      this.questions = this.generateQuestion()
      this.currentQuestionIndex = 0
  },
  methods: {
    generateQuestion: function () {
      let _questions = [];
      for (const key in this.alphabet) {
        _questions.push({
          question: key,
          answer: this.alphabet[key],
          userAnswer: null,
        });
      }
      this.questions = _questions;
    },
    shuffleQuestion: function () {
      let _questions = this.generateQuestion();
      this.questions = _.shuffle(_questions);
    },
    nextQuestion: function () {
      if (this.currentQuestionIndex <= this.questions.length - 1 - 1) {
        this.currentQuestionIndex += 1;
      }
    },
    resetQuestions: function () {
      this.currentQuestionIndex = 0;
      this.questions = [];
    },
  },
};
</script>

<style scoped>
</style>