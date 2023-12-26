<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <div id="app">
    <header>
      <div class="wrapper">
        <h1>tatau</h1>
        <p>
          <span><i>(verb) to count, calculate, add up, enumerate, tally.</i></span>
        </p>
        <p>
          A Javascript / Typescript package which translates between numerals and te reo Maori text.
        </p>
        <p>
          Tatau is dependency-less. Installing it will not add any additional dependencies to your
          project.
        </p>
        <nav>
          <a role="button" href="https://www.npmjs.com/package/tatau" target="_blank">NPM</a>
          <a role="button" href="https://github.com/jeff-goodman/tatau" target="_blank">GitHub</a>
          <a role="button" href="https://maoridictionary.co.nz/word/7653" target="_blank">Meaning</a>
        </nav>
      </div>
    </header>
    <div class="content">
      <RouterView />
    </div>
  </div>
</template>

<style scoped>
#app {
  display: flex;
}

header {
  flex: 1;
  padding-right: 3em;
}

.content {
  flex: 2;
}

nav {
  display: flex;
  justify-content: space-between;
  margin-top: 1em;
}
</style>
