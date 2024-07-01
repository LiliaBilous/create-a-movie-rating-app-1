<script setup>
import { ref } from "vue";
import { items } from "./movies.json";
import { StarIcon } from "@heroicons/vue/24/solid";

const movies = ref(items);

function updateRating(movieIndex, rating) {
  movies.value[movieIndex].rating = rating;
}
</script>

<template>
  <!-- This is where your template goes	-->
  <div class="movie__container">
    <div class="card-wrapper">
      <article class="movie__card" v-for="(item, movieIndex) in movies" :key="item.id">
        <div class="movie__img">
          <div class="movie-star-wrapper">
            <StarIcon
              :class="[item.rating ? 'text-yellow-500' : 'text-gray-500']"
            />
            <div class="movie-star">
              <span
                v-if="item.rating"
                class="star"
              >
                {{ item.rating }}
              </span>
              <span v-else class="not-rated">
                -
              </span>
            </div>
          </div>
          <img :src="item.image" alt="" />
        </div>
        <div class="movie__description">
          <header class="movie__header">
            <h3 class="movie__title">{{ item.name }}</h3>
            <div class="movie__label">
              <div v-for="gen in item.genres" :key="gen" class="movie__genres">
                {{ gen }}
              </div>
            </div>
          </header>
          <div class="movie__text">{{ item.description }}</div>
          <div class="movie__rating">
            <span class="rating">Rating ({{ item.rating }}/5)</span>
            <button
                v-for="star in 5"
                :key="star"
                class="star__button"
                :class="[
                  star <= item.rating ? 'text-yellow-500' : 'text-gray-500',
                ]"
                :disabled="star === item.rating"
                @click="updateRating(movieIndex, star)"
              >
                <StarIcon class="rating__star" />
              </button>
          </div>
        </div>
      </article>
    </div>
  </div>
</template>
