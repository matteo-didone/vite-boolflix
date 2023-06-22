<template>
    <nav class="navbar navbar-light bg-light">
        <div class="container-fluid">
            <!-- 
                v-model binds the input value to the data property searchQuery
                @click calls the method searchMovies when the button is clicked
            -->
            <input v-model="searchQuery" class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
            <button @click="searchMovies" class="btn btn-outline-success" type="button">Search</button>
        </div>
    </nav>

    <div class="movie-info">
        <h2>Movie Information:</h2>
        <ul>
            <!-- 
                v-for iterates over the movies array and displays the movie information
                :key is used to give each movie a unique identifier
            -->
            <li v-for="movie in movies" :key="movie.id">
                <!-- Copied .title, .orginal_title, .original_language, .vote_average from the API code, visualized using Postman -->
                <h3>{{ movie.title }}</h3>
                <p>Original Title: {{ movie.original_title }}</p>
                <p>Language: {{ movie.original_language }} </p>
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
            // Adding searchQuery and movies to the data object
            searchQuery: '',
            movies: [],
            countryCode: 'flag-icon flag-icon-',
        }
    },

    methods: {
        // Declaring searchMovies method, inside which there's the API call
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
                    // We update the movie array with the results properties of the data object
                    this.movies = data.results;
                })
                .catch(err => console.error(err));
        },
    }
}
</script>


<style lang="scss" scoped>
</style>    