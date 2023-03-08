<template>
    <main class="container">
        <ul class="grid">
        
            <Card/>
           
        </ul>
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
        Card
    }, 
    
}

</script>

<style lang="scss" scoped>
@use '../style/general.scss';

.grid{
    display: grid;
    grid-template-columns: repeat(4,1fr);
    gap: 40px;
}

</style>