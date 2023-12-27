<script setup lang="ts">
import { onMounted, ref } from 'vue';
import { tatau } from 'tatau';

const inputValue = ref(7);
const result = ref('');
const typingTimeoutId = ref(0);
const copySuccess = ref(false);

const handleInput = () => {
  let output = tatau(Number(inputValue.value));
  result.value = '';
  let charIndex = 0;
  clearTimeout(typingTimeoutId.value);

  const typeWriter = () => {
    const typingSpeed = 50;
    if (charIndex < output.length) {
      result.value += output.charAt(charIndex);
      charIndex++;
      typingTimeoutId.value = setTimeout(typeWriter, typingSpeed);
    }
  }
  typeWriter();
}

const copyToClipboard = async () => {
  const copyIndicatorDuration = 2000;
  const textToCopy = document.querySelector('.code-block-content')?.textContent || '';
  await navigator.clipboard.writeText(textToCopy);
  copySuccess.value = true;
  setTimeout(() => {
    copySuccess.value = false;
  }, copyIndicatorDuration);
}

onMounted(handleInput)
</script>

<template>
  <main>
    <input type="number" @input="handleInput" v-model="inputValue" />
    <div class="code-block">
      <span class="copy-icon material-symbols-outlined" @click="copyToClipboard">
        <span v-if="copySuccess">check_circle</span>
        <span v-else>content_copy</span>
      </span>
      <span class="code-block-content">
        <span class="light-purple">import</span> { <span class="light-blue">tatau</span> } <span class="light-purple">from</span> <span class="orange">'tatau'</span>; <br />
        <span class="blue">const</span> <span class="dark-blue">putanga</span> = <span class="yellow">tatau</span>({{ inputValue || 0 }});
      </span>
    </div>
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
  width: 90%;
  font-size: 2rem;
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 0.5rem;
  margin-bottom: 1rem;
}

#result {
  width: 90%;
  font-size: 2rem;
}

.code-block {
  width: 90%;
  background-color: #282c34;
  color: #abb2bf;
  padding: 20px;
  border-radius: 5px;
  font-family: 'Courier New', Courier, monospace;
  white-space: pre-wrap;
  position: relative;

  .copy-icon {
    position: absolute;
    top: 10px;
    right: 10px;
  }

  .copy-icon:hover {
    cursor: pointer;
  }

  .light-purple {
    color: #c678dd;
  }

  .light-blue {
    color: #61afef;
  }

  .blue {
    color: #4384f3;
  }

  .dark-blue {
    color: #0b67b3;
  }

  .yellow {
    color: #efef5a;
  }

  .orange {
    color: #d19a66;
  }
}
</style>
