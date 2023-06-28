<template>
    <div v-if="!showFinalView">
        <p>{{ points }} <span>{{ points > 0 ? 'points' : 'point' }}</span></p>
        <ul>
            <li v-for="question in showQuestions" :key="question.q">
                <p>Question {{ question.q }}</p>
                <p>{{ question.question }}</p>
                <QuizQuestions :questionOptions="question.options" @emitSelection="(option) => checkSelection(option)" />
                <button @click="checkAnswer(question)">Submit</button>
            </li>
        </ul>
    </div>
    <div v-else>
        <h2>Your total score is: {{ points }}</h2>
        <p v-if="showCorrectAnswer.length > 0">{{ showCorrectAnswer }}</p>
    </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import QuizQuestions from './Quiz-Questions.vue'

const showQuestions = ref([])
const selectedVal = ref('')
const points = ref(0)
const showFinalView = ref(false)
const showCorrectAnswer = ref([]);

const props = defineProps({
    quizQuestions: { type: Array, required: true }
});

console.log(props.quizQuestions);

function checkAnswer(question) {
    if (selectedVal.value) {
        if (question.answer === selectedVal.value) {
            points.value += 1;
        } else {
            showCorrectAnswer.value.push(question.answer)
        }

        showQuestions.value = props.quizQuestions.filter(questionIndex => questionIndex.q === question.q + 1)

        if (props.quizQuestions.length === question.q) {
            showFinalView.value = true;
            showQuestions.value = [];
        }
        
        selectedVal.value = ''
    }
    else {
        alert('Please select atleast 1 option')
        return
    }
}

function checkSelection(e) {
    selectedVal.value = e;
}

onMounted(() => {
    showQuestions.value = props.quizQuestions.filter(q => q.q === 1)
})
</script>

<style  scoped>
ul {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0;
    list-style-type: none;
}
</style>