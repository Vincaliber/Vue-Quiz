<script setup>
import { ref } from 'vue'
import QuizComponent from './components/Quiz-Component.vue';
import { questions } from './data/quiz-questions';
const quizQuestions = ref(questions)
</script>

<template>
  <div class="quiz-app">
    <h2>Quiz App</h2>
    <QuizComponent :quizQuestions="quizQuestions" />
  </div>
</template>

<style scoped>
.quiz-app{
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
</style>
