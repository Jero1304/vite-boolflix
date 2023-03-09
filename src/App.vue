<template>
  <Header @onSearch="fetchData"/>
  <Main/>
</template>

<script>
import Header from './components/Header.vue';
import Main from './components/Main.vue';
import store from './store';
import axios from 'axios';


export default{
  data(){
    return{
      store,
    }
  },
  components:{
    Header,
    Main,
  }, 
  methods:{
    fetchData(){
            console.log('fetch');
            this.fetchMovies()
            this.fetchSeries()
            store.search = ''
        },

    fetchMovies(){
      const url = this.store.config.URL + '/search/movie'
      axios.get(url,{
        params:{
          api_key: this.store.config.API_KEY,
          query:this.store.search,
          language: 'it-IT'
        }
      }).then((res)=>{
          const { results }= res.data
          this.store.movies = results
          console.log('fetch Movies');
          console.log(this.store.movies);
        }).catch((error)=>{
            console.log('ERROR:',error);
            this.store.movies = []
        })
    },

    fetchSeries(){
      const url = this.store.config.URL + '/search/tv'
      axios.get(url,{
        params:{
          api_key: this.store.config.API_KEY,
          query:this.store.search,
          language: 'it-IT'
        }
      }).then((res)=>{
          const { results }= res.data
          this.store.series = results
          console.log('fetch Series');
          console.log(this.store.series);
        }).catch((error)=>{
            console.log('ERROR:',error);
            this.store.series = []
        })
    },
  },
}
</script>


<style lang="scss" scoped>
@use './style/general.scss';

</style>
