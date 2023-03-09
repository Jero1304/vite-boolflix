<template>
    <div class="bg-main">
        <main class="container">
            <Card/> 
        </main>
    </div>
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
.bg-main{
    background-color: rgb(204, 204, 204);
}
.container{
    padding: 20px;
}

</style>