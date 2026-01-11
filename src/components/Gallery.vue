<script setup>
    import { ref, onMounted } from 'vue';
    import { RouterLink } from 'vue-router';
    import PhotoCard from './PhotoCard.vue';

    let photos = ref([]);

    onMounted(() => getPhotosFromLocalStorage());

    function getPhotosFromLocalStorage() {
        if (window.localStorage.getItem('photos') != null) {
            photos.value = JSON.parse(window.localStorage.getItem('photos'));
        }
    };
</script>

<template>
    <h2>Photos</h2>
    <p v-if="photos.length">Number of photos in the gallery: {{ photos.length }}</p>
    <ul v-if="photos.length">
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