<template>
    <div @mouseenter="getMovieCredits" class="single-card">
        <!-- Immagine di copertina -->
        <div class="front">
            <div>
                <!-- Immagine di copertina -->
                <img
                v-if="starWarsDetails.poster_path !== null" 
                :src="urlImages + starWarsDetails.poster_path" 
                :alt="starWarsDetails.original_title">
                <!-- Immagine sostitutiva -->
                <div v-else>
                    <img
                    src="https://media.istockphoto.com/vectors/error-page-or-file-not-found-icon-vector-id924949200?k=20&m=924949200&s=170667a&w=0&h=-g01ME1udkojlHCZeoa1UnMkWZZppdIFHEKk6wMvxrs=" 
                    alt="image not found">
                    <div
                    class="titolo-image"> 
                        {{starWarsDetails.title}}
                    </div>
                </div>
            </div>
        </div>
        <!-- Informazioni del film -->
        <ul 
        class="back">  
            <!-- Titolo -->
            <li>
                <span 
                class="bold">
                    Titolo:
                </span>
                {{starWarsDetails.title}}
            </li>
            <!-- Titolo originale -->
            <li>
                <span 
                class="bold">
                    Titolo originale:
                </span>
                {{starWarsDetails.original_title}}
            </li>
            <!-- Lingua -->
            <li>
                <span 
                class="bold">
                    Lingua:
                </span> 
                <img 
                class="flag" 
                :src="require('../assets/img/' + flagArray[activeFlag].flag)" 
                :alt="flagArray[activeFlag].lang"> 
            </li>
            <!-- Voto -->
            <li>
                <span 
                class="bold">
                    Voto:
                </span>
                <i 
                v-for="(element, index) in (0 + starVote)" 
                :key="index" 
                class="fas fa-star">
                </i>
                <i 
                v-for="(element, index) in (5 - starVote)" 
                :key="index" 
                class="far fa-star">
                </i>
            </li>
            <!-- Overview -->
            <li 
            v-if="starWarsDetails.overview">
                <span 
                class="bold">
                    Overview:
                </span>
                {{starWarsDetails.overview}}
            </li>
            <li 
            v-else>
                <span 
                class="bold">
                    Overview:
                </span>
                non disponibile
            </li>
            <!-- Attori Film -->
            <li 
            v-if="actorsArrayMovie.length > 0" >
                <span class="bold">
                    Attori:
                </span> 
                <div
                v-for="(element, index) in actorsArrayMovie" 
                :key="index">
                    {{element.name}}
                </div>
            </li>
            <li v-else>
                <span class="bold">
                    Attori:
                </span> 
                <span>
                    nessun dato
                </span>
            </li>
        </ul>
    </div>
</template>

<script>
import axios from 'axios';
    export default {
        name: 'StarWars',
        props: {
            starWarsDetails : Object,
            apiKey: String
        },
        data: function(){
            return{
                actorsArrayMovie: [],
                urlImages: 'https://image.tmdb.org/t/p/w342',
                flagArray: [
                    {
                        lang: 'it',
                        flag: 'ita.png'
                    },
                    {
                        lang: 'en',
                        flag: 'uk.png'
                    },
                    {
                        lang: 'es',
                        flag: 'spn.png'
                    },
                    {
                        lang: 'fr',
                        flag: 'frc.png'
                    },
                    {
                        lang: 'none',
                        flag: 'terra.png'
                    },
                ]
            }
        },
        methods: {
            getMovieCredits: function(){
                axios.get('https://api.themoviedb.org/3/movie/' + this.starWarsDetails.id +'/credits', {
                    params: {
                        api_key : this.apiKey
                    }
                }).then((response) => {
                    this.actorsArrayMovie = response.data.cast
                });
            },
        },
        computed: {
            activeFlag: function(){

                // Funzione per determinare quale bandiera mettere per la lingua

                let currentActiveFlag = null;

                if (this.starWarsDetails.original_language === 'it'){
                    currentActiveFlag = 0;
                    return currentActiveFlag
                } else if (this.starWarsDetails.original_language === 'en'){
                    currentActiveFlag = 1;
                    return currentActiveFlag
                } else if (this.starWarsDetails.original_language === 'es'){
                    currentActiveFlag = 2;
                    return currentActiveFlag
                } else if (this.starWarsDetails.original_language === 'fr'){
                    currentActiveFlag = 3;
                    return currentActiveFlag
                } else {
                    currentActiveFlag = 4;
                    return currentActiveFlag
                };
            },
            starVote: function(){

                // Funzione per trasformare il voto in decimali in voto in stelle

                let vote = Math.ceil(this.starWarsDetails.vote_average / 2);

                return vote;
            },
        },
    }

</script>

<style lang="scss" scoped>
.single-card{
    width: calc((100% / 2) - 20px);
    margin: 10px;
    border: 1px solid white;
    border-radius: 10px;
    text-align: center;
    color: white;
    flex-shrink: 0;
    cursor: pointer;
    overflow: hidden;
    max-height: 400px;
    overflow-y: auto;

    .front{
        display: block;

        .titolo-image{
            padding-top: 20px;
            font-size: 30px;
        }
    }

    .back{
        display: none;
        padding: 15px;
    }

    &:hover .front{
        display: none;
    }

    &:hover .back{
        display: block;
    }

    ul{
        list-style-type: none;

        li{
            font-size: 18px;
            margin-top: 10px;
            margin-bottom: 25px;
            // Soluzione trovata con Alessio per non modificare le dimensioni delle card all'hover a causa della grandezza dell'overview
            display: -webkit-box;
            -webkit-line-clamp: 5;
            -webkit-box-orient: vertical;
            overflow: hidden;
            word-break: normal;

            .flag{
                width: 25px;
                height: 20px;
                border-radius: 10px;
                vertical-align: middle;
            }

            .bold{
                font-weight: 600;
                padding-right: 10px;
                color: blueviolet;
                font-size: 20px;
            }
        }
    }
}


@media screen and (min-width: 576px) {
    .single-card{
        width:calc((100% / 2) - 20px)
    }
}

@media screen and (min-width: 768px){
    .single-card{
        width: calc((100% / 3) - 20px)
    }
};
@media screen and (min-width: 992px){
    .single-card{
        width: calc((100% / 5) - 20px)
    }
};
@media screen and (min-width: 1200px){
    .single-card{
        width: calc((100% / 7) - 20px)
    }
}
</style>