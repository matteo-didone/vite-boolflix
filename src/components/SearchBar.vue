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
                <p>Language: {{ movie.original_language }}
                    <img class="flag" :src="getFlag(movie.original_language)" />
                </p>
                <p>Rating: {{ movie.vote_average }}</p>
            </li>
        </ul>
    </div>

    <div class="tv-series-info">
        <h2>TV Series Information:</h2>
        <ul>
            <!-- 
                v-for iterates over the movies array and displays the movie information
                :key is used to give each movie a unique identifier
            -->
            <li v-for="serie in series" :key="serie.id">
                <!-- Copied .title, .orginal_title, .original_language, .vote_average from the API code, visualized using Postman -->
                <h3>{{ serie.title }}</h3>
                <p>Original Title: {{ serie.original_title }}</p>
                <p>Language: {{ serie.original_language }}
                    <img class="flag" :src="getFlag(serie.original_language)" />
                </p>
                <p>Rating: {{ serie.vote_average }}</p>
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
        this.searchMovies();
    },

    data() {

        return {
            store,

            // Adding searchQuery and movies to the data object
            searchQuery: '',

            movies: [],
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

        getFlag(country) {

            this.country = country.toLowerCase();

            if (country === "en") {
                return "https://flagsapi.com/GB/flat/64.png";
            } else if (country === "es") {
                return "https://flagsapi.com/ES/flat/64.png";
            } else if (country === "fr") {
                return "https://flagsapi.com/FR/flat/64.png";
            } else if (country === "it") {
                return "https://flagsapi.com/IT/flat/64.png";
            } else if (country === "ja") {
                return "https://flagsapi.com/JP/flat/64.png";
            } else if (country === "ko") {
                return "https://flagsapi.com/KR/flat/64.png";
            } else if (country === "pt") {
                return "https://flagsapi.com/PT/flat/64.png";
            } else if (country === "ru") {
                return "https://flagsapi.com/RU/flat/64.png";
            } else if (country === "zh") {
                return "https://flagsapi.com/CN/flat/64.png";
            } else if (country === "de") {
                return "https://flagsapi.com/DE/flat/64.png";
            } else if (country === "nl") {
                return "https://flagsapi.com/NL/flat/64.png";
            } else if (country === "sv") {
                return "https://flagsapi.com/SE/flat/64.png";
            } else if (country === "no") {
                return "https://flagsapi.com/NO/flat/64.png";
            } else if (country === "fi") {
                return "https://flagsapi.com/FI/flat/64.png";
            } else if (country === "da") {
                return "https://flagsapi.com/DK/flat/64.png";
            } else if (country === "hi") {
                return "https://flagsapi.com/IN/flat/64.png";
            } else if (country === "ar") {
                return "https://flagsapi.com/SA/flat/64.png";
            }

            return ""; // Return empty string if country code is not found
        }

    }
}
</script>


<style lang="scss" scoped>
.flag {
    height: 100%;
}
</style>    