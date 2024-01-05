<script setup lang="ts">
import DemoPanel from '@/components/DemoPanel.vue';
import NavBar from '@/components/NavBar.vue';
</script>

<template>
  <div class="links">
    <router-link to="/" class="nav-link">Home</router-link>
    <NavBar />
  </div>
  <DemoPanel :display-options="true" />
</template>

<style scoped>
.links {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  margin-bottom: 1em;
}

.nav-link {
  display: inline-block;
  padding: 10px 20px;
  text-decoration: none;
  color: black;
  background-color: white;
  transition: font-size 0.5s ease;
}

.nav-link:hover {
  font-size: 1.3em;
  transition: font-size 0.5s ease;
}
</style>
