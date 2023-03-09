<template>
    <ul class="grid">
        <li v-for="item in items" :key="item.id">

            <img :src="poster(item.poster)" alt="">
            
            <div v-if="item.title === item.originalTitle">
                <h3>{{ item.title }}</h3>
            </div>
            <div v-else>
                <h3>{{ item.title }}</h3>
                <h4>{{ item.originalTitle }}</h4>
            </div>
            
            <!-- lingua -->
            <p>
                Lingua: 
                <img 
                v-if="flagLang(item.language)"
                class="flag" 
                :src="flagLang(item.language)" 
                alt="">

                <span v-else>{{ item.language }}</span>
            </p>
            <!-- voto -->
            <p>
                Voto: 
                <font-awesome-icon icon="fa-solid fa-star" 
                v-for="i in 5" 
                :key="i" 
                :style="{ color: i <= starVote(item.vote) ? 'gold' : 'black' }" />
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
        // items() {
        //     return this.store.movies.concat(this.store.series)
        // },

        items() {
            const { series, movies} = this.store
            const items = this.store.movies.concat(this.store.series)

            return items.map((item) =>{
                const isMovie = item.title !== undefined

                return{
                    title: isMovie ? item.title : item.name,
                    originalTitle: isMovie ? item.original_title : item.original_name,
                    language: item.original_language,
                    vote: item.vote_average,
                    isMovie: isMovie,
                    poster: item.poster_path,
                }
            })
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