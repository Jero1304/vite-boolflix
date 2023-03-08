<template>
    <li v-for="movie in store.movies" :key="movie.id">
        <h3>{{ movie.title }}</h3>
        <h4>{{ movie.original_title }}</h4>
        <p>{{ movie.language }}</p>
        <p>{{ movie.vote_average }}</p>
    </li>
</template>

<script>
import store from '../store'
export default{
    data(){
        return{
            store
        }
    },
    props:{
        type: Object,
        required: true,
    },
    
}
</script>

<style>

</style>