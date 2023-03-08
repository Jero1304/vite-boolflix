<template>
    <ul class="grid">
        <li v-for="item in combinedData" :key="item.id">
            <img :src="Image" alt="">
            <h3>{{ item.title ? item.title : item.name}}</h3>
            <h4>{{ item.original_title ? item.original_title : item.original_name }}</h4>
            <p>{{ item.language ? item.language : item.original_language }}</p>
            <p>{{ item.vote_average}}</p>
            
        </li>
        {{ Language }}
    </ul>
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
    computed:{
        combinedData() {
            return this.store.movies.concat(this.store.series)
        },
        Language(){
            return 
        },
        Image(){
            return this.item.poster_path
        }
    },
    methods:{

    }
    
}
</script>

<style lang="scss" scoped>
@use '../style/general.scss';
.grid{
    display: grid;
    grid-template-columns: repeat(4,1fr);
    gap: 40px;

    li{
        border: 1px solid black;
        border-radius: 20px;
        padding: 20px;
    }
}

</style>