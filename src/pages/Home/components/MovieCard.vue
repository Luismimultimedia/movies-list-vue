<script setup>

import { ref } from 'vue';
import { StarIcon } from "@heroicons/vue/24/solid";

const props = defineProps({
    movies: {
        type: Array,
        required: false,
        default: () => [],
    }
});
const mappedMovies = ref(props.movies);
const setRating = (movieId, rating) => {
    mappedMovies.value = mappedMovies.value.map((movie) => {
        const { id } = movie || {};
        if (id === movieId) {
            movie.rating = rating;
        }
        return movie;
    });
};
</script>

<template>
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-2">
        <article class="movie-card__container" v-for="movie in mappedMovies">
            <picture class="movie-card__media">
                <img :src="movie?.image" />
            </picture>
            <div class="movie-card__information">
                <h2 class="font-sans font-bold text-3xl">{{ movie?.name }}</h2>
                <div v-for="genre in movie?.genres" class="movie-card__chips">
                    <p>{{ genre }}</p>
                </div>
                <p class="movie-card__description font-sans font-semibold">{{ movie?.description }}</p>
                <div class="movie-card__rating justify-self-end">
                    <p>Rating: ({{ movie.rating }}/5)</p>
                    <button
                        v-for="item in 5"
                        @click="setRating(movie?.id, item)"
                    >
                        <StarIcon :class="[
                            'movie-card__rating--star',
                            {'movie-card__rating--star-disable': (movie.rating < item)}
                        ]" />
                    </button>
                </div>
            </div>
        </article>
    </div>
</template>

<style lang="scss">
.movie-card {
    &__container {
        width: 100%;
        border-radius: 4px;
        background-color: white;
    }

    &__media {
        img {
            border-radius: 4px 4px 0 0;
            width: 100%;
            height: 550px;
            object-fit: cover;
        }
    }

    &__information {
        padding: 6px;
    }

    &__chips {
        display: inline-block;
        background-color: blueviolet;
        color: white;
        padding: 2px 6px;
        width: auto;
        margin-right: 5px;
        border-radius: 20px;
    }

    &__description {
        margin-top: 10px;
    }

    &__rating {
        display: flex;
        align-items: center;
        margin-top: 20px;

        p {
            margin-right: 10px;
        }

        &--star {
            fill: rgb(197, 172, 58);
            height: 20px;
            width: 20px;
            margin-right: 5px;
            &-disable {
                fill: rgb(170, 168, 159);
            }
        }
    }
}
</style>