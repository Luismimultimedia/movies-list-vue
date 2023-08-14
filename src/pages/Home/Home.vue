<script setup>
import { computed, onMounted } from 'vue';

// components
import MovieCard from './components/MovieCard.vue';

// props
const props = defineProps({
    movies: {
        type: Array,
        default: () => [],
        required: true,
    }
});

// computed
const ratingMovies = computed(() => {
    return props.movies.sort((a,b) => b.rating - a.rating);
});

</script>

<template>
    <section>
        <MovieCard :movies="ratingMovies" />
    </section>
</template>

<style lang="">
    
</style>