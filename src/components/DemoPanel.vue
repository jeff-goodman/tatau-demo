<script setup lang="ts">
import { computed, defineEmits, onMounted, ref, watchEffect } from 'vue';
import { tatau, type TatauOptions } from 'tatau';

defineProps<{
  displayOptions: boolean;
}>();

const emit = defineEmits({
  'update:classMode': null,
  'update:ordinalInput': null,
  'update:ordinalOutput': null,
});

const classMode = ref(false);
const ordinalInput = ref(false);
const ordinalOutput = ref(false);

const updateClassMode = (value: boolean) => {
  classMode.value = value;
  handleInput();
};

const updateOrdinalInput = (value: boolean) => {
  ordinalInput.value = value;
  handleInput();
};

const updateOrdinalOutput = (value: boolean) => {
  ordinalOutput.value = value;
  handleInput();
};

watchEffect(() => {
  // Emit an event whenever classMode changes
  emit('update:classMode', classMode.value);
  emit('update:ordinalInput', ordinalInput.value);
  emit('update:ordinalOutput', ordinalOutput.value);
});

const tatauOptions = computed(() => {
  return {
    ...(ordinalInput.value && { ordinalInput: ordinalInput.value }),
    ...(ordinalOutput.value && { ordinalOutput: ordinalOutput.value }),
  } as TatauOptions;
});

const tatauOptionsString = computed(() => {
  let options = JSON.stringify(tatauOptions.value, null, 2);
  options = options.replace(/"([^(")"]+)":/g, '$1:');
  return options;
});

const randomInt = Math.floor(Math.random() * (1000 - 10 + 1)) + 10;
const inputValue = ref(randomInt);
const result = ref('');
const typingTimeoutId = ref(0);
const copySuccess = ref(false);

const handleInput = () => {
  let output = tatau(Number(inputValue.value), tatauOptions.value);
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
  };
  typeWriter();
};

const copyToClipboard = async () => {
  const copyIndicatorDuration = 2000;
  const textToCopy = document.querySelector('.code-block-content')?.textContent || '';
  await navigator.clipboard.writeText(textToCopy);
  copySuccess.value = true;
  setTimeout(() => {
    copySuccess.value = false;
  }, copyIndicatorDuration);
};

function isObjectEmpty(obj: object) {
  return Object.keys(obj).length === 0;
}

onMounted(handleInput);
</script>

<template>
  <main>
    <div class="options-panel" v-if="displayOptions">
      <div class="options-panel-row">
        <div class="split-button-label">Usage Type</div>
        <div class="split-button">
          <input
            type="radio"
            id="function"
            value="false"
            v-model="classMode"
            @change="updateClassMode(false)"
          />
          <label for="function">Function</label>
          <input
            type="radio"
            id="class"
            value="true"
            v-model="classMode"
            @change="updateClassMode(true)"
          />
          <label for="class">Class</label>
        </div>
      </div>

      <div class="options-panel-row">
        <div class="split-button-label">Ordinal Input</div>
        <div class="split-button">
          <input
            type="radio"
            id="ordinalInputFalse"
            value="false"
            v-model="ordinalInput"
            @change="updateOrdinalInput(false)"
            disabled
          />
          <label for="ordinalInputFalse">False</label>
          <input
            type="radio"
            id="ordinalInputTrue"
            value="true"
            v-model="ordinalInput"
            @change="updateOrdinalInput(true)"
            disabled
          />
          <label for="ordinalInputTrue">True</label>
        </div>
      </div>

      <div class="options-panel-row">
        <div class="split-button-label">Ordinal Output</div>
        <div class="split-button">
          <input
            type="radio"
            id="ordinalOutputFalse"
            value="false"
            v-model="ordinalOutput"
            @change="updateOrdinalOutput(false)"
          />
          <label for="ordinalOutputFalse">False</label>
          <input
            type="radio"
            id="ordinalOutputTrue"
            value="true"
            v-model="ordinalOutput"
            @change="updateOrdinalOutput(true)"
          />
          <label for="ordinalOutputTrue">True</label>
        </div>
      </div>
    </div>
    <input type="number" @input="handleInput" v-model="inputValue" />
    <p id="result">{{ result }}</p>
    <div class="code-block" v-if="displayOptions">
      <span class="copy-icon material-symbols-outlined" @click="copyToClipboard">
        <span v-if="copySuccess">check_circle</span>
        <span v-else>content_copy</span>
      </span>
      <span class="code-block-content">
        <span class="light-purple">import</span> {
        <span class="light-blue"><span v-if="classMode">Tatau</span><span v-else>tatau</span></span>
        } <span class="light-purple">from</span> <span class="orange">'tatau'</span>; <br />
        <span v-if="classMode"
          ><span class="dark-blue">const</span> <span class="blue">myTatau</span> =
          <span class="dark-blue">new</span> <span class="yellow">Tatau(</span
          ><span v-html="tatauOptionsString"></span><span class="yellow">)</span>;<br
        /></span>
        <span class="blue">const</span> <span class="dark-blue">putanga</span> =
        <span class="yellow"><span v-if="classMode">myTatau.</span>tatau(</span>{{ inputValue || 0
        }}<span v-if="!classMode && !isObjectEmpty(tatauOptions)"
          >, <span v-html="tatauOptionsString"></span></span
        ><span class="yellow">)</span>;
      </span>
    </div>
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

/* Code Block */
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

.options-panel {
  width: 90%;
  display: flex;
  flex-direction: column;
  margin-bottom: 0.5rem;
}

.options-panel-row {
  flex: 1;
  display: flex;
  flex-direction: row;
  margin-right: 10px;
}

/* Split Button */

.split-button-label {
  width: 100cw;
  margin-right: 10px;
  align-self: center;
  flex: 1;
}

.split-button {
  flex: 3;
  display: flex;
  width: 100%;
  overflow: hidden;
  /* border-radius: 0.5rem; */
  margin-bottom: 0.5rem;
}

.split-button input[type='radio'] {
  display: none;
}

.split-button label {
  position: relative;
  flex: 1;
  padding: 10px;
  text-align: center;
  background-color: white;
  border: 1px solid #ccc;
  cursor: pointer;  
  border-radius: 0.5rem 0 0 0.5rem;
} 

.split-button label:last-child {
  border-radius: 0 0.5rem 0.5rem 0;
}

.split-button input[type='radio']:checked + label {
  border: 1px solid black !important;
}

.split-button input[type='radio']:disabled + label {
  background-color: white; /**  #f0f0f0; */
  color: #aaa;
  cursor: not-allowed;
}
</style>
