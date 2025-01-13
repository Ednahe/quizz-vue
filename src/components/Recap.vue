<script setup>
import { computed } from 'vue';

const props = defineProps({
    quizz: Object,
    reponses: Array
})

const score = computed(() => {
    return props.quizz.questions.reduce((count, question, index) => {
        if (question.correct === props.reponses[index]) {
            return count + 1;
        }
        return count;
    }, 0)
})

</script>

<template>
    <h1>Recap</h1>
    <p>
        Score : {{ score }}/{{ quizz.questions.length }}
    </p>
</template>