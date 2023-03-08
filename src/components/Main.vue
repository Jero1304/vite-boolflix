<template>
    <main class="container">
        <Card/> 
    </main>
</template>

<script>
import store from '../store'
import Card from './Card.vue'
export default{
    data(){
        return{
            store,
        }
    },
    components:{
        Card,
    }, 
    
}

</script>

<style lang="scss" scoped>
@use '../style/general.scss';



</style>