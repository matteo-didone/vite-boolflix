<template>
    <header>
        <NavBar />
    </header>
</template>

<script>
import { store } from '../store.js'
import NavBar from './NavBar.vue'

export default {
    name: 'AppHeader',

    components: {
        NavBar
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