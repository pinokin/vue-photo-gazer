<script setup>
    import { ref, onMounted } from 'vue';
    import { RouterLink } from 'vue-router';
    import PhotoCard from './PhotoCard.vue';

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

            photos.value = data;
        
        } catch (error) {
            console.warn(error);
        }
    }
</script>

<template>
    <h2>Photos</h2>
    <p>Number of photos in the gallery: {{ photos.length }}</p>
    <ul>
        <li v-for="photo in photos" :key="photo.id">
            <RouterLink :to="`/photo/${photo.id}`">
                <PhotoCard v-bind="photo"></PhotoCard>
            </RouterLink>
        </li>
    </ul>
</template>

<style scoped>
    ul {
        padding: 0;
        display: grid;
        gap: 1rem;
        grid-template-columns: repeat(5, 1fr);
        grid-auto-rows: minmax(200px, auto);
    }

    li {
        list-style-type: none;
    }
</style>