<script setup>
    import { ref, onMounted } from 'vue';
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
    <div v-if="photos.length" class="tag-container">
        <small>Number of photos in the gallery: <b>{{ photos.length }}</b></small>
    </div>
    <ul v-if="photos.length">
        <li v-for="photo in photos" :key="photo.id">
            <PhotoCard v-bind="photo"></PhotoCard>
        </li>
    </ul>
</template>

<style scoped>
    .tag-container {
        display: flex;
        justify-content: end;
        padding-block-end: 1rem;
    }

    .tag-container small {
        background-color: var(--pico-muted-color);
        color: var(--pico-primary-inverse);
        padding: 0.25rem 0.5rem;
        border-radius: 0.25rem;
    }

    ul {
        padding: 0;
        display: grid;
        gap: 1rem;
        grid-template-columns: repeat(auto-fill, minmax(min(200px, 100%), 1fr));
    }

    li {
        list-style-type: none;
    }
</style>