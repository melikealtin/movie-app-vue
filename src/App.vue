<template>
  <header>
    <router-link to="/">
      <h1><span>Vue</span>Movies</h1>
    </router-link>
  </header>

  <main>
    <RouterView />
  </main>
</template>

<script setup>
import { RouterView } from 'vue-router'
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;

  &::selection {
    background: transparentize(#42b883, 0.5);
  }
}

body {
  background: #202035;
}
a {
  text-decoration: none;
}

header {
  display: flex;
  align-content: center;
  justify-content: center;
  padding: 10px 16px;
  background-color: #1b1b30;
  box-shadow: 0px 0px 6px rgba(0, 0, 0, 0.4);

  h1 {
    color: #fff;
    font-size: 28px;

    span {
      color: #6051d2;
    }
  }
}
</style>
