<template>
    <header>
        <SearchBar />
    </header>
</template>

<script>
import { store } from '../store.js'
import SearchBar from './SearchBar.vue';

export default {
    name: 'AppHeader',

    components: {
        SearchBar
    },

    data() {

        return {
            store,
        };
    },

    methods: {

    }
}
</script>


<style lang="scss" scoped></style>    