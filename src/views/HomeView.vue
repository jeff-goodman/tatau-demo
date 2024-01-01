<script setup lang="ts">
import DemoPanel from '@/components/DemoPanel.vue';
import NavBar from '@/components/NavBar.vue';

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
       <NavBar />
      </div>
    </header>
    <div class="content">
      <DemoPanel /> 
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

</style>
