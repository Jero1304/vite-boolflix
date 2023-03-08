<template>
    <ul class="grid">
        <li v-for="item in combinedData" :key="item.id">
            <img :src="poster(item.poster_path)" alt="">
            <h3>Titolo: {{ item.title ? item.title : item.name}}</h3>
            <h4>Titolo Originale: {{ item.original_title ? item.original_title : item.original_name }}</h4>
            <p>
                Lingua: 
                <!-- {{ item.language ? item.language : item.original_language }} -->
                <img 
                v-if="flagLang(item.language ? item.language : item.original_language)"
                class="flag" 
                :src="flagLang(item.language ? item.language : item.original_language)" 
                alt="">

                <span v-else>{{ item.language ? item.language : item.original_language }}</span>
            </p>
            <p>
                Voto: 
                <i 
                class="fa-solid fa-star"
                v-for="i in 5" 
                :key="i" 
                :style="{ color: i <= starVote(item.vote_average) ? 'gold' : 'black' }" 
                ></i>
            </p>        
        </li>
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
    },
    methods:{
        poster(image){
            const url='https://image.tmdb.org/t/p/w342'
            return image = url + image
            // console.log(image);
        },
        flagLang(lang){
            // console.log(lang);
            switch (lang) {
                case 'en':
                    return '../../public/img/gb.png';
                case 'ja':
                    return '../../public/img/jp.png';
                case 'it':
                    return '../../public/img/it.png';    
            }
        },
        starVote(vote){
            vote = vote/2;
            vote = Math.ceil(vote)
            // console.log(vote);
            return vote
        }

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
        .flag{
            width: 20px;
        }
    }
}

</style>