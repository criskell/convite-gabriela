<script setup lang="ts">
import { ref } from 'vue';

const noButton = ref<HTMLButtonElement | null>(null);
const step = ref(1)

const moveButton = () => {
  const button = noButton.value;
  if (button) {
    const container = button.parentElement;
    if (container) {
      const containerRect = container.getBoundingClientRect();
      const maxX = containerRect.width - button.offsetWidth;
      const maxY = containerRect.height - button.offsetHeight;

      let randomX, randomY;
      do {
        randomX = Math.random() * maxX;
        randomY = Math.random() * maxY;
      } while (
        Math.abs(randomX - parseFloat(button.style.left || '0')) < 50 ||
        Math.abs(randomY - parseFloat(button.style.top || '0')) < 50
      );

      button.style.position = 'absolute';
      button.style.left = `${randomX}px`;
      button.style.top = `${randomY}px`;
    }
  }
};

const accept = () => {
  step.value = 2;

};
</script>
<template>
  <div v-if="step === 1" class="container">
    <h1>maju, gostaria de saber se você quer ir no CEU comigo ver a semi do futsal!! 🥰</h1>
    <div class="buttons">
      <button class="accept-button" @click="accept">Sim</button>
      <button
        ref="noButton"
        @mouseenter="moveButton"
        class="no-button"
      >
        Não
      </button>
    </div>
  </div>
  <div v-if="step === 2" class="container">
    <h2>eu sabia que você não iria resistir! kakaka</h2>
    <h3>mandarei mais informações no wpp. um beijo, linda! 🥰</h3>

  </div>
</template>



<style>
.container {
  text-align: center;
  margin-top: 10%;
  font-family: Arial, sans-serif;
}

h1 {
  font-size: 2rem;
  margin-bottom: 2rem;
}

.buttons {
  position: relative;
  width: 300px;
  height: 200px;
  margin: 0 auto;

}

.accept-button {
  color: #ffffff;
}

button {
  padding: 10px 20px;
  font-size: 1rem;
  cursor: pointer;
  border: 2px solid #333;
  border-radius: 5px;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #f0f0f0;
}

.no-button {
  background-color: #ffcccc;
  position: absolute;
}
</style>
