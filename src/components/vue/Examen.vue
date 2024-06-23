<script setup>
import { ref } from 'vue';

const questions = ref([
  {
    question: "¿Qué biblioteca de Vue se importa al inicio del script?",
    answers: [
      { answer: "vue-router", correct: false },
      { answer: "ref", correct: true },
      { answer: "vuex", correct: false },
      { answer: "vue-test-utils", correct: false }
    ]
  },
  {
    question: "¿Qué colores se incluyen en el array `firstQuestion`?",
    answers: [
      { answer: "rojo, azul, amarillo, verde", correct: true },
      { answer: "rojo, azul, naranja, verde", correct: false },
      { answer: "rojo, púrpura, amarillo, verde", correct: false },
      { answer: "rojo, azul, negro, verde", correct: false }
    ]
  },
  {
    question: "¿Cuál es el valor inicial de `boxState`?",
    answers: [
      { answer: "true", correct: false },
      { answer: "false", correct: true },
      { answer: "undefined", correct: false },
      { answer: "null", correct: false }
    ]
  }
]);

const currentQuestionIndex = ref(0);
const selectedAnswer = ref(null);
const isCorrect = ref(false);

function selectAnswer(answer) {
  selectedAnswer.value = answer;
  isCorrect.value = answer.correct;
}

function nextQuestion() {
  if (currentQuestionIndex.value < questions.value.length - 1) {
    currentQuestionIndex.value++;
    selectedAnswer.value = null;
    isCorrect.value = false;
  }
}
</script>

<template>
  <div>
    <div v-if="currentQuestionIndex < questions.length">
      <div class="bg-slate-400 flex m-auto w-[800px] h-[500px] justify-center items-center">
        <h2 class="mx-auto text-white font-bold text-2xl">{{ questions[currentQuestionIndex].question }}</h2>
      </div>
      <div class="grid grid-cols-2 grid-rows-2 gap-2">
        <div v-for="(answer, index) in questions[currentQuestionIndex].answers" :key="index" @click="selectAnswer(answer)" class="text-center text-white font-semibold text-xl cursor-pointer my-1 p-2 bg-[#e0e0e0] hover:bg-[#b0b0b0]">
          {{ answer.answer }}
        </div>
      </div>
      <div class="flex justify-between p-4">
        <div v-if="selectedAnswer" class="bg-blue-600 rounded-lg border p-4 text-white font-semibold">
          <p>{{ isCorrect ? 'Correcto!' : 'Incorrecto' }}</p>
        </div>
        <button @click="nextQuestion" class="bg-green-600 rounded-lg border p-4 text-white font-semibold">Siguiente</button>
      </div>
    </div>
    <div v-else>
      <p class="bg-slate-400 flex m-auto w-[800px] h-[500px] justify-center items-center text-white font-bold text-2xl">¡Has completado el cuestionario!</p>
    </div>
  </div>
</template>

