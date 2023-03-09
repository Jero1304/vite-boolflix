<template>
    <header class="bg-header">
        <div class="container">
            <div class="header">
                <div class="logo">
                    <h1>BOOLFLIX</h1>
                </div>
                <div class="search-bar">
                    <input 
                    @keyup.enter="$emit('onSearch')" 
                    v-model="store.search" 
                    type="text" 
                    placeholder="Cerca Film"
                    >
                </div>
            </div>
        </div>
    </header>
</template>

<script>
import store from '../store'
export default{
    data(){
        return{
            store,
            
        }
    }, 
}

</script>

<style lang="scss" scoped>
@use '../style/general.scss';
.bg-header{
    background-color: black;
    .header{
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
        padding: 20px;
        .logo{
            color: red;
        }
        .search-bar{

            input{
                padding: 7px;
                border-radius: 20px;
            }
        }
    }
}

</style>