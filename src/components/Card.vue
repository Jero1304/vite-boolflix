<template>
    <ul class="grid">
        <li v-for="item in items" :key="item.id">
            <div class="card">

                <img :src="poster(item.poster)" alt="">
                <div class="overlay">
                    <!-- titolo -->
                    <div class="title">
                        <div v-if="item.title === item.originalTitle">
                            <h3>Titolo: 
                                <p>{{ item.title }} </p>
                            </h3>
                        </div>
                        <div v-else>
                            <h3>Titolo: 
                                <p>{{ item.title }} </p>
                            </h3>                            
                            <h4>Titolo originale:
                                <p>{{ item.originalTitle }}</p>
                            </h4>
                        </div>          
                    </div>

                    <!-- lingua -->
                    <p class="language">
                        Lingua: 
                        <img 
                        v-if="flagLang(item.language)"
                        class="flag" 
                        :src="flagLang(item.language)" 
                        alt="">
                        
                        <span v-else>{{ item.language }}</span>
                    </p>
                    
                    <!-- voto -->
                    <p class="voto">
                        Voto: 
                        <font-awesome-icon icon="fa-solid fa-star" 
                        v-for="i in 5" 
                        :key="i" 
                        :style="{ color: i <= starVote(item.vote) ? 'gold' : 'white' }" />
                    </p>    
                    
                    <!-- trama -->
                    <p class="trama">Trama: 
                        <p>{{ item.overview }}</p>
                    </p>
                    
                </div>

            </div>
        </li>
    </ul>
</template>

<script>
import store from '../store'
export default{
    data(){
        return{
            store,
            isHover:false,
        }
    },
    props:{
        type: Object,
        required: true,
    },
    computed:{
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
                    overview: item.overview,
                }
            })
        },
    },

    methods:{
        poster(image){
            const url='https://image.tmdb.org/t/p/w342'
            image = url + image
            return this.store.img = image
            // console.log('image',image);
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
        color: white;
        border: 1px solid black;
        .card{
            // background-image: url(${store});
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
            height: 350px;
            position: relative;
            img{
                width: 100%;
                height: 100%;
                object-fit: cover;
            }
            .overlay{
                display: none;
                padding: 15px;
            }
            &:hover{
                .overlay {
                    color: lightgrey;
                    display: block;
                    height: 100%;
                    width: 100%;
                    position: absolute;
                    top: 0;
                    overflow-y: auto;
                    background-color: rgba(0, 0, 0, 0.8);
                    object-fit: cover;
                    .title{
                        h3{
                            padding-bottom: 8px;
                        }
                        font-size: 18px;
                        p{
                            font-size: 14px;
                            color: rgb(165, 165, 165);
                        }
                        padding-bottom: 10px;
                    }
                    .language,.voto,.trama{
                        font-size: 14px;
                        padding-bottom: 10px;
                        font-weight: bold;
                        
                        .flag{
                            width: 20px;
                            height: 15px;
                        }
                    }
                    .trama > p, .language > span{
                        font-size: 15px;
                        font-weight: 100;
                    }
                }
            }
        }
        
    }
}

</style>