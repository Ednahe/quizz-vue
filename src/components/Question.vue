<script setup>
const props = defineProps({
    question: Object
})
</script>

<template>
    <div class="question">
        <h3>{{ question.question }}</h3>
        <ul>
            <li v-for="(choices, index) in question.choices" :key="choices">
                <label :for="`reponse${index}`">
                    <input :id="`reponse${index}`" type="radio" name="reponse">
                    {{ choices }}
                </label>
            </li>
        </ul>
        <button>Question suivante</button>
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