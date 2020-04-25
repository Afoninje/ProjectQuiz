<template>
  <div class="container-app">
    <div class="container-quiz">
      <div class="quiz-header">
        <h1>Quiz Topic</h1>
      </div>
      <div class="main-quiz" v-for="(element,index) in questions.slice(a,b)" :key="index">
        <div class="box-question">
          <h2>Question {{b}}/{{questions.length}}</h2>
          <p>{{element.question}}</p>
        </div>
        <div class="box-suggestion">
          <ul>
            <li v-for="(item,index) in element.suggestions" :key="index" :class="select ? check(item): '' ">{{item.suggestion}}</li>
          </ul>
        </div>
      </div>
      <div class="box-score"></div>
      <div class="quiz-footer">
        <div class="box-button">
          <button>Skip</button>
          <button>Next</button>
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
      select: false
    };
  },
  methods: {
    selectResponse() {
      this.select = true;
    },
    check(status) {
      if (status.correct) {
        return "correct";
      } else {
        return "incorrect";
      }
    }
  }
};
</script>