<script setup lang="ts">
import { RouterView } from 'vue-router'
</script>

<template>
  <h1>tatau</h1>
  <p>
    <span><i>(verb) to count, calculate, add up, enumerate, tally.</i></span>
  </p>
  <div id="app">
    <header>
      <div class="wrapper">
        <p>
          A Javascript / Typescript package which translates between numerals and te reo Māori text.
        </p>
        <nav>
          <a role="button" href="https://www.npmjs.com/package/tatau" target="_blank">NPM</a>
          <a role="button" href="https://github.com/jeff-goodman/tatau" target="_blank">GitHub</a>
          <a role="button" href="https://maoridictionary.co.nz/word/7653" target="_blank"
            >Meaning</a
          >
        </nav>
      </div>
    </header>
    <div class="content">
      <RouterView />
    </div>
  </div>
</template>

<style scoped>
h1 {
  margin-bottom: 0;
}

p {
  margin-top: 0;
}

#app {
  display: flex;
  flex-direction: row;
}

header {
  flex: 1;
  padding-right: 3em;
}

.content {
  flex: 2;
}

@media screen and (max-width: 768px) {
  #app {
    flex-direction: column-reverse;
  }
}

nav {
  display: flex;
  justify-content: space-between;
  margin-top: 1em;
}
</style>
