<template>
    <main>
        <div v-if="movies.length > 0 || tvseries.length > 0">
            <div>
                <h2>
                    FILM
                </h2>
            </div>
            <div 
            class="container">
                <SingleCardCommon 
                v-for="(element, index) in movies" 
                :key="index" 
                :element="element" />
            </div>
            <div class="serietv">
                <h2>
                    SERIE TV
                </h2>
            </div>
            <div  
            class="container">
                <SingleCardCommon 
                v-for="(element, index) in tvseries" 
                :key="index" 
                :element="element"/>
            </div>
        </div>
        <div 
        v-else class="no-result">
            <h3>
                Nessun risultato
            </h3>
        </div>
    </main>
</template>

<script>
import SingleCardCommon from './SingleCardCommon.vue';

export default {
    name: 'Main',
    components: {
        SingleCardCommon
    },
    props: {
        movies : Array,
        tvseries: Array,
        text : String,
    },
}
</script>

<style scoped lang="scss">
main{
    height: calc(100% - 100px);
    background-color: black;
    color: white;

    .serietv{
        padding-top: 100px;
    }

    h2{
        padding: 30px;
    }
    
    .container{
        width: 90%;
        margin: auto;
        display: flex;
        overflow-x: auto;
    }

    .no-result{
        font-size: 40px;
        margin-top: 30px;
        display: flex;
        justify-content: center;
    }
}
</style>