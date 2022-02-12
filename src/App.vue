<template>
  <div id="nav" class="py-4 text-3xl mb-4 text-gray-400 text-center">
    <router-link :to="{ name: 'Home' }">Projects</router-link> |
    <router-link :to="{ name: 'Add' }">Add Projects</router-link>
  </div>
  <router-view />
</template>

<style>
body {
  background: #f2f2f2;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 0 auto;
  max-width: 600px;
  color: #555;
}
</style>
