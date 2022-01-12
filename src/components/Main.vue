<template>
    <main>
        <div>
            <h2>Risultati della ricerca per: {{text}}</h2>
            <div v-if="movies.length > 0">
                <div>
                    <h2>Film:</h2>
                </div>
                <div class="container">
                    <SingleCardMovies v-for="(element, index) in movies" :key="index" :element="element" />
                </div>
                <div>
                    <h2>Serie TV:</h2>
                </div>
                <div class="container">
                    <SingleCardTv v-for="(element, index) in tvseries" :key="index" :element="element"/>
                </div>
            </div>
            <div v-else class="no-result">
                <h3>Nessun risultato</h3>
            </div>
        </div>
    </main>
</template>

<script>
import SingleCardMovies from './SingleCardMovies.vue';
import SingleCardTv from './SingleCardTv.vue';

export default {
    name: 'Main',
    components: {
        SingleCardMovies,
        SingleCardTv,
    },
    props: {
        movies : Array,
        tvseries: Array,
        text : String
    },
}
</script>

<style scoped lang="scss">
main{
    height: calc(100% - 100px);

    h2{
        padding: 30px;
    }
    
    .container{
        width: 90%;
        margin: auto;
        display: flex;
        flex-wrap: wrap;
    }

    .no-result{
        font-size: 40px;
        margin-top: 30px;
        display: flex;
        justify-content: center;
    }
}
</style>