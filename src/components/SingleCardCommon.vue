<template>
    <div @mouseenter="mouseEnterFunctions" class="single-card">
        <!-- Immagine di copertina -->
        <div class="front">
            <div>
                <!-- Immagine di copertina -->
                <img
                v-if="element.poster_path !== null" 
                :src="urlImages + element.poster_path" 
                :alt="element.original_title">
                <!-- Immagine sostitutiva -->
                <div v-else>
                    <img
                    src="https://media.istockphoto.com/vectors/error-page-or-file-not-found-icon-vector-id924949200?k=20&m=924949200&s=170667a&w=0&h=-g01ME1udkojlHCZeoa1UnMkWZZppdIFHEKk6wMvxrs=" 
                    alt="image not found">
                    <div
                    class="titolo-image" 
                    v-if="element.title">
                        {{element.title}}
                    </div>
                    <div
                    class="titolo-image" 
                    v-else>
                        {{element.name}}
                    </div>
                </div>
            </div>
        </div>
        <!-- Informazioni del film -->
        <ul class="back">  
            <!-- Titolo -->
            <li 
            v-if="element.title">
                <span class="bold">Titolo:</span>
                {{element.title}}
            </li>
            <li
            v-else>
                <span class="bold">Titolo:</span>
                {{element.name}}
            </li>
            <li
            v-if="element.original_title">
                <span class="bold">Titolo originale:</span>
                {{element.original_title}}
            </li>
            <li
            v-else>
                <span class="bold">Titolo originale:</span> 
                {{element.original_name}}
            </li>
            <!-- Lingua -->
            <li>
                <span class="bold">Lingua:</span> 
                <img 
                class="flag" 
                :src="require('../assets/img/' + flagArray[activeFlag].flag)" 
                :alt="flagArray[activeFlag].lang"> 
            </li>
            <!-- Voto -->
            <li>
                <span class="bold">Voto:</span>
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
            v-if="element.overview">
                <span class="bold">Overview:</span>
                <div>
                    {{element.overview}}
                </div>
            </li>
            <li v-else>
                <span class="bold">
                    Overview:
                </span>
                non disponibile
            </li>
            <!-- Attori Film -->
            <li v-if="element.title">
                <div
                v-if="actorsArrayMovie.length > 0">
                    <span class="bold">
                        Attori:
                    </span> 
                    <div
                    v-for="(element, index) in actorsArrayMovie" 
                    :key="index">
                        {{element.name}}
                    </div>
                </div>
                <div v-else>
                    <span class="bold">
                        Attori:
                    </span> 
                    <span>
                        nessun dato
                    </span>
                </div>
            </li>
            <!-- Attori Tv-->
            <li v-else>
                <div 
                v-if="actorsArrayTv.length > 0">
                    <span class="bold">
                        Attori:
                    </span>
                    <div
                    v-for="(elementTv, index) in actorsArrayTv"
                    :key="index">
                        {{elementTv.name}}
                    </div>
                </div>
                <div v-else>
                    <span class="bold">
                        Attori:
                    </span> 
                    <span>
                        nessun dato
                    </span>
                </div>
            </li>
            <!-- Generi -->
            <li v-if="element.title">
                <span class="bold">
                    Generi:
                </span>
                <div>
                    {{genreStringMovie}}
                </div>
            </li>
            <li v-else>
                <span class="bold">
                    Generi:
                </span>
                <div>
                    {{genreStringTv}}
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: 'SingleCardCommon',
    props:{
        element: Object,
        apiKey: String
    },
    data: function(){
        return{
            actorsArrayMovie: [],
            actorsArrayTv: [],
            genresList: [],
            genreListTv: [],
            genreStringMovie: '',
            genreStringTv: '',
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
    methods:{
        // Funzione che attiva le altre funzioni al mouseenter
        mouseEnterFunctions: function(){
            if(this.element.title){
                this.getMovieCredits();
                this.genreId();
            } else if(this.element.name){
                this.getTvCredits();
                this.genreIdTv()
            }
        },
        // Funzione che chiama l'API per la lista di attori nei film
        getMovieCredits: function(){
            axios.get('https://api.themoviedb.org/3/movie/' + this.element.id +'/credits', {
                params: {
                    api_key : this.apiKey
                }
            }).then((response) => {
                this.actorsArrayMovie = response.data.cast
            });
        },
        // Funzione che chiama l'API per la lista di attori nelle serie tv
        getTvCredits: function(){
            axios.get('https://api.themoviedb.org/3/tv/' + this.element.id + '/credits', {
                params: {
                    api_key : 'eb32925ee4340f32b75ef0f48a3de4d6'
                }
            }).then((response) => {
                this.actorsArrayTv = response.data.cast
            })
        },
        // Funzione per determinare il genere dall'id del film
        genreId: function(){
            this.genresList.forEach((genres) =>{
                if(this.element.genre_ids.includes(genres.id)){
                    this.genreStringMovie = genres.name
                }
            })
        },
        // Funzione per determinare il genere dall'id delle serie tv
        genreIdTv: function(){
            this.genreListTv.forEach((genresTv) => {
                if(this.element.genre_ids.includes(genresTv.id)){
                    this.genreStringTv = genresTv.name
                }
            })
        }

    },
    created: function(){
        // Chiamata API per prendere lista generi serie tv
        axios.get('https://api.themoviedb.org/3/genre/tv/list', {
            params: {
                api_key :  'eb32925ee4340f32b75ef0f48a3de4d6',
            } 
        }).then((response) => {
            this.genreListTv = response.data.genres
        });

        // Chiamata API per prendere lista generi film
        axios.get('https://api.themoviedb.org/3/genre/movie/list',{
            params: {
                api_key : 'eb32925ee4340f32b75ef0f48a3de4d6',
            }
        }).then((response) => {
            this.genresList = response.data.genres
        })
    },
    computed: {
        activeFlag: function(){

            // Funzione per determinare quale bandiera mettere per la lingua

            let currentActiveFlag = null;

            if (this.element.original_language === 'it'){
                currentActiveFlag = 0;
                return currentActiveFlag
            } else if (this.element.original_language === 'en'){
                currentActiveFlag = 1;
                return currentActiveFlag
            } else if (this.element.original_language === 'es'){
                currentActiveFlag = 2;
                return currentActiveFlag
            } else if (this.element.original_language === 'fr'){
                currentActiveFlag = 3;
                return currentActiveFlag
            } else {
                currentActiveFlag = 4;
                return currentActiveFlag
            };
        },
        starVote: function(){

            // Funzione per trasformare il voto in decimali in voto in stelle

            let vote = Math.ceil(this.element.vote_average / 2);

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
    font-weight: 200;
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

    // Effetti all'hover
    &:hover .front{
        display: none;
    }

    &:hover .back{
        display: block;
    }

    ul{
        list-style-type: none;

        li{
            margin-top: 10px;
            margin-bottom: 25px;
            font-size: 18px;
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

// Mediaquery
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