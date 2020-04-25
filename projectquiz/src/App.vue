<template>
  <div class="container-app">
    <div class="container-quiz">
      <div class="quiz-header">
        <h1>Quiz Topic</h1>
      </div>
      <div
        class="main-quiz"
        v-for="(element,index) in questions.slice(a,b)"
        :key="index"
        v-show="quiz"
      >
        <div class="box-question">
          <h2>Question {{b}}/{{questions.length}}</h2>
          <p>{{element.question}}</p>
        </div>
        <div class="box-suggestion">
          <ul>
            <li
              v-for="(item,index) in element.suggestions"
              :key="index"
              :class="select ? check(item): '' "
              @click="selectResponse(item)"
            >{{item.suggestion}}</li>
          </ul>
        </div>
      </div>
      <div class="box-score" v-if="score_show">
        <h2>Your Score Is:</h2>
        <h2>{{score}}/{{questions.length}}</h2>
        <div class="btn-restart">
          <button @click="restartQuiz">
            Restart
            <i class="fas fa-sync-alt"></i>
          </button>
        </div>
      </div>
      <div class="quiz-footer">
        <div class="box-button">
          <button @click="skipQuestion">Skip</button>
          <button @click="nextQuestion">Next</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      questions: [
        {
          question: "Q1",
          suggestions: [
            { suggestion: "1", correct: true },
            { suggestion: "2" },
            { suggestion: "3" },
            { suggestion: "4" }
          ]
        },
        {
          question: "Q2",
          suggestions: [
            { suggestion: "1" },
            { suggestion: "2", correct: true },
            { suggestion: "3" },
            { suggestion: "4" }
          ]
        },
        {
          question: "Q3",
          suggestions: [
            { suggestion: "1" },
            { suggestion: "2" },
            { suggestion: "3", correct: true },
            { suggestion: "4" }
          ]
        },
        {
          question: "Q4",
          suggestions: [
            { suggestion: "1" },
            { suggestion: "2" },
            { suggestion: "3" },
            { suggestion: "4", correct: true }
          ]
        }
      ],
      a: 0,
      b: 1,
      select: false,
      score: 0,
      quiz: true,
      score_show: false
    };
  },
  methods: {
    selectResponse(e) {
      this.select = true;

      if (e.correct) {
        this.score++;
      }
    },
    check(status) {
      if (status.correct) {
        return "correct";
      } else {
        return "incorrect";
      }
    },
    nextQuestion() {
      if (this.questions.length - 1 == this.a) {
        this.score_show = true;
        this.quiz = false;
      } else {
        this.a++;
        this.b++;
        this.select = false;
      }
    },
    skipQuestion() {
      if (this.questions.length - 1 == this.a) {
        this.score_show = true;
        this.quiz = false;
      } else {
        this.a++;
        this.b++;
      }
    },
    restartQuiz() {
      Object.assign(this.$data, this.$options.data());
    }
  }
};
</script>