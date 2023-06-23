<template>
    <nav class="navbar navbar-light bg-light">
        <div class="container-fluid">
            <!-- 
                v-model binds the input value to the data property searchQuery
                @click calls the method searchMovies when the button is clicked
            -->
            <input v-model="searchQuery" class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
            <!-- A button can only trigger one method when clicked in Vue -->
            <button @click="searchMoviesAndTvSeries" class="btn btn-outline-success" type="button">Search</button>
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
                <p>Rating Halfed and Rounded: {{ convertMovieRating(movie.vote_average) }}</p>
                <div class="star-rating-wrapper">
                    <span v-for="starsFilled in totalStars" :key="starsFilled">
                        <font-awesome-icon v-if="starsFilled <= convertMovieRating(movie.vote_average)"
                            :icon="['fas', 'star']" class="filled" />
                        <font-awesome-icon v-else :icon="['fas', 'star']" />
                    </span>
                </div>
                <p> <img class="movieCover" :src="getMovieCover(movie)" /> </p>
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
            <li v-for="serie in tvSeries" :key="serie.id">
                <!-- Copied .name, .orginal_title, .original_language, .vote_average from the API code, visualized using Postman -->
                <h3>{{ serie.name }}</h3>
                <p>Original Title: {{ serie.original_name }}</p>
                <p>Language: {{ serie.original_language }}
                    <img class="flag" :src="getFlag(serie.original_language)" />
                </p>
                <p>Rating: {{ serie.vote_average }}</p>
                <p>Rating Halfed and Rounded: {{ convertTvSerieRating(serie.vote_average) }}</p>
                <div class="star-rating-wrapper">
                    <span v-for="starsFilled in totalStars" :key="starsFilled">
                        <font-awesome-icon v-if="starsFilled <= convertTvSerieRating(serie.vote_average)"
                            :icon="['fas', 'star']" class="filled" />
                        <font-awesome-icon v-else :icon="['fas', 'star']" />
                    </span>
                </div>
                <p> <img class="tvSerieCover" :src="getTvSerieCover(serie)" /> </p>
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

    data() {

        return {
            store,

            // Adding searchQuery and movies to the data object
            searchQuery: '',

            // Adding movies array to the data object
            movies: [],

            // Adding series array to the data object
            tvSeries: [],

            totalStars: 5,
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
        },

        // Declaring searchMovies method, inside which there's the API call
        searchTvSerie() {
            const options = {
                method: 'GET',
                headers: {
                    accept: 'application/json',
                    Authorization: 'Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI4ZjYwMDQ3Y2RlYWZmNWM0NmYxZTc3MDdlMDc3YWY0MCIsInN1YiI6IjY0OTJjM2IxNjVlMGEyMDEyNWY5ZjgyZiIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.zuGfWxv_Hgil7FBEhmMq0e7sRe2NH5D0lXZnDpLTOV8'
                }
            };

            fetch(`https://api.themoviedb.org/3/search/tv?include_adult=false&language=en-US&page=1&query=${this.searchQuery}`, options)
                .then(response => response.json())
                .then(data => {
                    // We update the tvSeries array with the results properties of the data object
                    this.tvSeries = data.results;
                })
                .catch(err => console.error(err));
        },

        // Declaring searchMoviesAndTvSeries method, inside which there's the searchMovies and searchTvSerie methods
        // Why? Because a user can search for movies and tv series at the same time by clicking the search button
        // A search button in Vue can only trigger one method when clicked, so we need to create a method that calls the other two
        searchMoviesAndTvSeries() {
            this.searchMovies();
            this.searchTvSerie();
        },

        getMovieCover(movie) {
            if (movie.poster_path) {
                return `https://image.tmdb.org/t/p/w342${movie.poster_path}`;
            }

            else if (movie.backdrop_path) {
                return `https://image.tmdb.org/t/p/w342${movie.backdrop_path}`;
            }

            else {
                return `https://ih1.redbubble.net/image.1030805420.6483/flat,750x,075,f-pad,750x1000,f8f8f8.jpg`
            }
        },

        getTvSerieCover(tvSerie) {
            if (tvSerie.poster_path) {
                return `https://image.tmdb.org/t/p/w342${tvSerie.poster_path}`;
            }

            else if (tvSerie.backdrop_path) {
                return `https://image.tmdb.org/t/p/w342${tvSerie.backdrop_path}`;
            }

            else {
                return `https://ih1.redbubble.net/image.1030805420.6483/flat,750x,075,f-pad,750x1000,f8f8f8.jpg`
            }
        },

        // We then convert the decimal rating from 1 to 10 into a whole number from 1 to 5, allowing us to display a number of filled stars on the screen ranging from 1 to 5, leaving the rest empty (we can find the icons in FontAwesome). We always round up to the next whole number and do not handle half-filled icons (or half-empty ones :P).
        convertMovieRating(voteAverage) {
            const halfRating = Math.ceil(voteAverage / 2);

            return halfRating;
        },

        convertTvSerieRating(voteAverage) {
            const halfRating = Math.ceil(voteAverage / 2);
            return halfRating;
        },


    }
}
</script>


<style lang="scss" scoped>
.flag {
    height: 100%;
}

.star-rating-wrapper {
    display: flex;
    align-items: center;
}

.fa-star.filled {
    color: gold;
}

.fas.fa-star {
    color: lightgray;
}
</style>    