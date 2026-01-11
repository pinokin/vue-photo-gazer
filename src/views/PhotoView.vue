<script setup>
  import { ref, onMounted } from 'vue';
  import { useRoute } from 'vue-router';
  import { RouterLink } from 'vue-router';
  
  let route = useRoute();
  let photo = ref({});

  onMounted(() => getPhotoByRouteParam());

  function getPhotoByRouteParam() {

    if (window.localStorage.getItem('photos') == null) {
      return;
    }

    if (route.params.id == null) {
      return;
    }

    let photos = JSON.parse(window.localStorage.getItem('photos'));
    
    let photoById = photos.find((photo) => photo.id === parseInt(route.params.id));

    if (photoById != undefined) {
      photo.value = photoById;
    }
  };
</script>

<template>
  <hgroup>
    <h2>Photo #{{ photo.id }}</h2>
    <p>{{ photo.title }}</p>
  </hgroup>
  <img :src="photo.imageUrl" :alt="photo.title" :title="photo.title" width="600" />
  <p>
    <RouterLink :to="{ name: 'home' }">Back to gallery</RouterLink>
  </p>
</template>
