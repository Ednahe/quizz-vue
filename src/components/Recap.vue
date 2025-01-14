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

const victory = computed(() => score.value >= props.quizz.minimum_score)

</script>

<template>
    <h1>Recap</h1>
    <p>
        {{ victory ? quizz.succes_message : quizz.fail_message }}
    </p>
    <p>
        Score : {{ score }}/{{ quizz.questions.length }}
    </p>
</template>