<script setup>
    const props = defineProps({
        id: Number,
        title: String,
        thumbnailUrl: String,
    });
</script>

<template>
    <img :src="props.thumbnailUrl" :alt="props.title" :title="props.title" width="300" />
</template>