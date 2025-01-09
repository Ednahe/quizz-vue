<script setup>
import { ref, computed } from 'vue';

const props = defineProps({
    question: Object
})

const emits = defineEmits(['reponse']);
const reponse = ref(null);
const noReponse = computed(() => reponse.value !== null)
</script>

<template>
    <div class="question">
        <h3>{{ question.question }}</h3>
        <ul>
            <li v-for="(choices, index) in question.choices" :key="choices">
                <label :for="`reponse${index}`">
                    <input :id="`reponse${index}`" type="radio" name="reponse" v-model="reponse" :value="choices">
                    {{ choices }}
                </label>
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