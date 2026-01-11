<script setup>
  import { ref, onMounted } from 'vue';
  import { useRoute } from 'vue-router';
  
  let route = useRoute();
  let photo = ref({});

  onMounted(() => getPhotoByRouteParam());

  function getPhotoByRouteParam() {

    if (window.localStorage.getItem('photos') == null) {
      return null;
    }

    if (route.params.id == null) {
      return null;
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
    <h1>Photo #{{ photo.id }}</h1>
  </hgroup>
</template>
