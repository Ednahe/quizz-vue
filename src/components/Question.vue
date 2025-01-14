<script setup>
import { ref, computed } from 'vue';
import { shuffleArray } from '../functions/array';
import Reponse from './Reponse.vue';

const props = defineProps({
    question: Object
})

const emits = defineEmits(['reponse']);
const reponse = ref(null);
const noReponse = computed(() => reponse.value !== null)
const randomChoices = computed(() => shuffleArray(props.question.choices))
</script>

<template>
    <div class="question">
        <h3>{{ question.question }}</h3>
        <ul>
            <li v-for="(choice, index) in randomChoices" :key="choice">
                <Reponse :id="`reponse${index}`" :disabled="noReponse" :value="choice" v-model="reponse"/>
            </li>
        </ul>
        {{ reponse }}
        <button :disabled="!noReponse" @click="emits('reponse', reponse)">Question suivante</button>
    </div>
</template>

<style>
.question {
    padding-top: 2rem;
}

.question button {
    margin-left: auto;
    display: block;
}
</style>