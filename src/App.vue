<script setup>
  import { ref, onMounted, onUnmounted } from 'vue';
  import { RouterLink, RouterView } from 'vue-router'

  let isLoading = ref(false);

  onMounted(() => getPhotos());
  onUnmounted(() => clearLocalStorage());

  async function getPhotos() {

    if (window.localStorage.getItem('photos')) {
      // Photos has already been fetched
      return;
    }

    try {
      isLoading = true;

      let response = await
        fetch('https://jsonplaceholder.typicode.com/photos?_page=1&_limit=25');
      
      if (!response.ok) {
        throw "API returned status code " + response.status;
      }

      let data = await response.json();

      data.forEach((photo) => {
        photo.imageUrl = "https://picsum.photos/seed/" + photo.id + "/600.webp";
        photo.thumbnailUrl = "https://picsum.photos/seed/" + photo.id + "/300.webp";
      });

      window.localStorage.setItem('photos', JSON.stringify(data));

      isLoading = false;
    
    } catch (error) {
        console.warn(error);
    }
  }

  function clearLocalStorage() {
    window.localStorage.removeItem('photos');
  }
</script>

<template>
  <header>
    <hgroup class="container">
      <h1>Photo Gazer</h1>
      <p>A simple image gallery built with Vue.</p>
    </hgroup>
  </header>

  <main class="container">
    <span v-if="isLoading" aria-busy>Getting photos...</span>
    <RouterView />
  </main>

  <footer>
    <div class="container">
      <p><a href="https://github.com/pinokin/vue-photo-gazer">Code in Github</a></p>
    </div>
  </footer>
</template>
