<script setup>
    import { RouterLink } from 'vue-router';

    const props = defineProps({
        id: Number,
        title: String,
        thumbnailUrl: String,
    });
</script>

<template>
    <div class="photo-card">
        <RouterLink :to="`/photo/${props.id}`" class="photo-card-link">
            <img :src="props.thumbnailUrl" :alt="props.title" :title="props.title" width="300" />
        </RouterLink>
    </div>
</template>

<style scoped>

    .photo-card {
        position: relative;
        box-shadow: 0 0.2rem 0.2rem rgba(0, 0, 0, 0.3);
    }

    .photo-card:hover,
    .photo-card:focus,
    .photo-card:focus-within {
        box-shadow: 0 0.5rem 0.5rem rgba(0, 0, 0, 0.3);
        transform: scale(1.01);
    }

    .photo-card-link {
        position: static;
        text-decoration: none;
        color: var(--pico-primary);
    }

    .photo-card-link:focus {
        outline: none;
    }

    .photo-card-link::before {
        content: '';
        display: block;
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
    }

    .photo-card-link:focus::before {
        outline: 2px solid var(--pico-primary);
        outline-offset: 0.05rem;
    }

</style>