<template>
    <nav class="navbar navbar-light bg-light">
        <div class="container-fluid">
            <input v-model="searchQuery" class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
            <button @click="searchMovies" class="btn btn-outline-success" type="button">Search</button>
        </div>
    </nav>

    <div class="movie-info">
        <h2>Movie Information:</h2>
        <ul>
            <li v-for="movie in movies" :key="movie.id">
                <h3>{{ movie.title }}</h3>
                <p>Original Title: {{ movie.original_title }}</p>
                <p>Language: {{ movie.original_language }}</p>
                <p>Rating: {{ movie.vote_average }}</p>
            </li>
        </ul>
    </div>
</template>

<script>
import { store } from '../store.js'

export default {
    name: 'SearchBar',

    components: {

    },

    created() {

    },

    data() {

        return {
            store,
            searchQuery: '',
            movies: [],
        }
    },

    methods: {
        searchMovies() {
            // Implemented API call to TMDB
            const options = {
                method: 'GET',
                headers: {
                    accept: 'application/json',
                    Authorization: 'Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI4ZjYwMDQ3Y2RlYWZmNWM0NmYxZTc3MDdlMDc3YWY0MCIsInN1YiI6IjY0OTJjM2IxNjVlMGEyMDEyNWY5ZjgyZiIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.zuGfWxv_Hgil7FBEhmMq0e7sRe2NH5D0lXZnDpLTOV8'
                }
            };

            fetch(`https://api.themoviedb.org/3/search/movie?include_adult=false&language=en-US&page=1&query=${this.searchQuery}`, options)
                .then(response => response.json())
                .then(data => {
                    this.movies = data.results;
                })
                .catch(err => console.error(err));
        }
    }
}
</script>


<style lang="scss" scoped></style>    