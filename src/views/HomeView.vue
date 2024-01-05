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
        <nav>
          <router-link to="/options" class="nav-link">Full Demo</router-link>
        </nav>
      </div>
    </header>
    <div class="content">
      <DemoPanel :display-options="false" />
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
  margin-bottom: 2rem;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
}

nav {
  display: flex;
  flex-direction: row;
  justify-content: center;
  margin-top: 1rem;
}

.nav-link {
  display: inline-block;
  width: 100%;
  text-align: center;
  padding: 10px 20px;
  margin: 0 5px;
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

@media screen and (max-width: 768px) {
  #app {
    flex-direction: column-reverse;
  }
}
</style>
