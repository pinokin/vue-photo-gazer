<script setup>
    import { ref, onMounted } from 'vue';
    import PhotoCard from './PhotoCard.vue';

    let numberOfPhotos = ref(0);
    let photos = ref([]);

    onMounted(() => getPhotos());

    async function getPhotos() {

        try {

            let response = await
                fetch('https://jsonplaceholder.typicode.com/photos?_page=1&_limit=25');
            
            if (!response.ok) {
                throw "API returned status code " + response.status;
            }

            let data = await response.json();

            numberOfPhotos.value = data.length;
            photos.value = data;
        
        } catch (error) {
            console.warn(error);
        }
    }
</script>

<template>
    <h2>Photos</h2>
    <p>Number of photos in the gallery: {{ numberOfPhotos }}</p>
    <div v-for="photo in photos" :key="photo.id">
        <PhotoCard v-bind="photo"></PhotoCard>
    </div>
</template>