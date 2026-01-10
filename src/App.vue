<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <p>This is the header</p>
  </header>

  <main>
    <RouterView />
  </main>

  <footer>
    <p>This is the footer</p>
  </footer>
</template>
