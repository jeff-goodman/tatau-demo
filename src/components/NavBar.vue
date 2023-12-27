<template>
  <nav>
    <a class="nav-link" href="https://www.npmjs.com/package/tatau" target="_blank">NPM</a>
    <a class="nav-link" href="https://github.com/jeff-goodman/tatau" target="_blank">GitHub</a>
    <a class="nav-link" href="https://maoridictionary.co.nz/word/7653" target="_blank">Meaning</a>
  </nav>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'NavBar'
});
</script>

<style scoped>
nav {
  display: flex;
  justify-content: space-between;
  margin-top: 1em;
}

.nav-link {
  display: inline-block;
  padding: 10px 20px;
  text-decoration: none;
  color: black;
  background-color: white;
  border: 1px solid transparent;
  border-radius: 5px;
  transition: border 0.5s ease;
}

.nav-link:hover {
  border: 1px solid black;
}

</style>