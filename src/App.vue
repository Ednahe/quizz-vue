<script setup>
import { onMounted, ref } from "vue";
import Quizz from "./components/Quizz.vue";

const quizz = ref(null);
const state = ref("loading");

onMounted(() => {
  fetch("/quizz.json")
    .then((response) => {
      if (response.ok) {
        return response.json();
      }
      throw new Error("Impossible de récupérer le json");
    })
    .then((data) => {
      quizz.value = data;
      state.value = "idle";
    })
    .catch((e) => {
      state.value = "erreur";
    });
});
</script>

<template>
  <div class="container">
    <div v-if="state === 'erreur'">
      <p>impossible de charger le quizz</p>
    </div>
    <div :aria-busy="state === 'loading'">
      <Quizz :quizz="quizz" v-if="quizz" />
    </div>
  </div>
</template>
