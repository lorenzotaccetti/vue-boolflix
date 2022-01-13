<template>
    <main>
        <div class="intestazione">Inizia a seguire la saga di Star Wars direttamente dalla nostra app</div>
        <div class="container">
            <StarWars v-for="(starWarsDetails, index) in starWarsFilm" :key="index" :starWarsDetails="starWarsDetails" />
        </div>
        <div 
        v-if="movies.length > 0 || tvseries.length > 0">
            <div class="paddingtop">
                <div class="intestazione">
                    Film trovati per: '{{text}}'
                </div>
            </div>
            <div 
            class="container">
                <SingleCardCommon 
                v-for="(element, index) in movies" 
                :key="index" 
                :element="element" />
            </div>
            <div class="paddingtop">
                <div class="intestazione">
                    Serie tv trovate per: '{{text}}'
                </div>
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
        v-else 
        class="no-result">
            <h3 
            class="paddingtop"
            v-if="text === ''">
                Inizia a cercare qualcosa che ti interessa
            </h3>
            <h3
            v-else
            class="paddingtop">
                Nessun risultato
            </h3>
        </div>
    </main>
</template>

<script>
import SingleCardCommon from './SingleCardCommon.vue';
import StarWars from './StarWars.vue'

export default {
    name: 'Main',
    components: {
        SingleCardCommon,
        StarWars
    },
    props: {
        movies : Array,
        tvseries: Array,
        text : String,
        starWarsFilm : Array
    },
}
</script>

<style scoped lang="scss">
main{
    height: calc(100% - 100px);
    background-color: black;
    color: white;
    margin: 50px 0;

    .paddingtop{
        padding-top: 100px;
    }

    .intestazione{
        font-size: 30px;
        font-weight: bold;
        padding: 30px;
        text-transform: uppercase;
        color: #e20a13;
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
        color: #e20a13;
    }
}
</style>