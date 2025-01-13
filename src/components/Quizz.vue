<script setup>
import { computed, ref } from "vue";
import Progress from "./Progress.vue"
import Question from "./Question.vue";
import Recap from "./Recap.vue";

const props = defineProps({
    quizz: Object
})

const reponses = ref(props.quizz.questions.map(() => null));
const state = ref('question');
const step = ref(0);
const question = computed(() => props.quizz.questions[step.value]);

const addReponse = (reponse) => {
    reponses.value[step.value] = reponse;
    if (step.value === props.quizz.questions.length - 1) {
        state.value = 'recap';
    } else {
        step.value++;
    }
}
</script>

<template>
    <div>
        <h1>{{ quizz.title }}</h1>
        <Progress :value="step" :max="quizz.questions.length" />
        <Question :key="question.question" :question="question" v-if="state === 'question'" @reponse="addReponse"/>
        <Recap v-if="state === 'recap'" :reponses="reponses" :quizz="quizz"/>
        {{ reponses }}
    </div>
</template>