<script setup>
import { ref } from 'vue';

const questions = ref([
  {
    question: "¿Cuál es el compañero Digimon de Tai?",
    answers: [
      { answer: "Gabumon", correct: false },
      { answer: "Agumon", correct: true },
      { answer: "Patamon", correct: false },
      { answer: "Gomamon", correct: false }
    ]
  },
  {
    question: "¿Cuál es la evolución mega de Agumon?",
    answers: [
      { answer: "MetalGreymon", correct: false },
      { answer: "WarGreymon", correct: true },
      { answer: "SkullGreymon", correct: false },
      { answer: "Greymon", correct: false }
    ]
  },
  {
    question: "¿Cuál es el Digimon con forma de ángel que acompaña a T.K.?",
    answers: [
      { answer: "Angemon", correct: true },
      { answer: "Devimon", correct: false },
      { answer: "Angewomon", correct: false },
      { answer: "Seraphimon", correct: false }
    ]
  },
  {
    question: "¿Quién es el líder de los Dark Masters?",
    answers: [
      { answer: "Piedmon", correct: true },
      { answer: "Machinedramon", correct: false },
      { answer: "MetalSeadramon", correct: false },
      { answer: "Puppetmon", correct: false }
    ]
  },
  {
    question: "¿Cuál es el Digimon que tiene forma de cactus?",
    answers: [
      { answer: "Palmon", correct: false },
      { answer: "Togemon", correct: true },
      { answer: "Lillymon", correct: false },
      { answer: "Tentomon", correct: false }
    ]
  }
]);

const currentQuestionIndex = ref(0);
const selectedAnswer = ref(null);
const isCorrect = ref(false);
const correctAnswersCount = ref(0);

function selectAnswer(answer) {
  if (selectedAnswer.value) return;

  selectedAnswer.value = answer;
  isCorrect.value = answer.correct;
  if (answer.correct) {
    correctAnswersCount.value++;
  }
}

function nextQuestion() {
  if (currentQuestionIndex.value < questions.value.length - 1) {
    currentQuestionIndex.value++;
    selectedAnswer.value = null;
    isCorrect.value = false;
  } else {
    currentQuestionIndex.value++;
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
    <div v-else class="bg-slate-400 flex m-auto w-[800px] h-[500px] justify-center items-center text-white font-bold text-2xl">
      <div>
        <p>¡Has completado el cuestionario!</p>
        <p>Respuestas correctas: {{ correctAnswersCount }}</p>
      </div>
    </div>
  </div>
</template>
