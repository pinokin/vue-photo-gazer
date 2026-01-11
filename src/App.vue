<script setup>
  import { onMounted, onUnmounted } from 'vue';
  import { RouterView } from 'vue-router'

  onMounted(() => getPhotos());
  onUnmounted(() => clearLocalStorage());

  async function getPhotos() {

    if (window.localStorage.getItem('photos')) {
      // Photos has already been fetched
      return;
    }

    try {
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
    <p>This is the header</p>
  </header>

  <main>
    <RouterView />
  </main>

  <footer>
    <p>This is the footer</p>
  </footer>
</template>
