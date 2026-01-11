<script setup>
  import { onMounted } from 'vue';
  import { RouterView } from 'vue-router'

  onMounted(() => getPhotos());

  async function getPhotos() {

      try {

          let response = await
              fetch('https://jsonplaceholder.typicode.com/photos?_page=1&_limit=25');
          
          if (!response.ok) {
              throw "API returned status code " + response.status;
          }

          let data = await response.json();

          window.localStorage.setItem('photos', JSON.stringify(data));
      
      } catch (error) {
          console.warn(error);
      }
  }
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
