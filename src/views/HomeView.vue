<script setup lang="ts">
import { onMounted, ref } from 'vue';
import { tatau } from 'tatau';

let inputValue = ref(1234567);
let result = ref('');
let typingTimeoutId = ref(0);

const handleInput = () => {
  let output = tatau(Number(inputValue.value));
  result.value = '';
  let i = 0;
  clearTimeout(typingTimeoutId.value);

  const typeWriter = () => {
    if (i < output.length) {
      result.value += output.charAt(i);
      i++;
      typingTimeoutId.value = setTimeout(typeWriter, 50);
    }
  }
  typeWriter();
}

onMounted(handleInput)
</script>

<template>
  <main>
    <input type="number" @input="handleInput" v-model="inputValue" />
    <p id="result">{{ result }}</p>
  </main>
</template>

<style scoped>
main {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
}

input {
  width: 90cw;
  font-size: 2rem;
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 0.5rem;
  margin-bottom: 1rem;
}

#result {
  width: 90cw;
  font-size: 2rem;
}
</style>
