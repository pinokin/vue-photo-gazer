<script setup>
    import { computed } from 'vue';

    const props = defineProps({
        id: Number,
        title: String,
    });

    let imageUrl = computed(() => {
        let urlWithId = "https://picsum.photos/seed/" + props.id + "/300/300";
        return urlWithId;
    });

</script>

<template>
    <article>
        <img :src="imageUrl" :alt="props.title" :title="props.title" width="300" />
    </article>
</template>