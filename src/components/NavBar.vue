<template>
    <SearchBar />
</template>

<script>
import { store } from '../store.js'
import SearchBar from './SearchBar.vue';

export default {
    name: 'NavBar',

    components: {
        SearchBar
    },

    data() {

        return {
            store,
        }
    },

    methods: {

    }
}
</script>


<style lang="scss" scoped>

</style>    