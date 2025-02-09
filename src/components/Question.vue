<script setup>
import { ref, computed, onMounted } from "vue";
import { shuffleArray } from "../functions/array";
import Reponse from "./Reponse.vue";

const props = defineProps({
  question: Object,
});

const emits = defineEmits(["reponse"]);
const reponse = ref(null);
const noReponse = computed(() => reponse.value !== null);
const randomChoices = computed(() => shuffleArray(props.question.choices));

let timer;

const onReponse = (e) => {
    reponse.value = e.currentTarget.value;
    clearTimeout(timer);
    timer = setTimeout(() => {
        emits('reponse', reponse.value)
    }, 1000)
}

onMounted(() => {
    timer = setTimeout(() => {
        emits('reponse', reponse.value)
    }, 3000)
})

onMounted(() => {
    clearTimeout(timer)
})
</script>

<template>
  <div class="question">
    <h3>{{ question.question }}</h3>
    <ul>
      <li v-for="(choice, index) in randomChoices" :key="choice">
        <Reponse
          :id="`reponse${index}`"
          :disabled="noReponse"
          :value="choice"
          @change="onReponse"
          :correctReponse="question.correct"
        />
      </li>
    </ul>
    {{ reponse }}
    <!-- <button :disabled="!noReponse" @click="emits('reponse', reponse)">
      Question suivante
    </button> -->
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
