<template>
    <div class="single-card">
        <!-- Immagine di copertina -->
        <ul class="front">
            <li>
                <img
                v-if="starWarsDetails.poster_path !== null" 
                :src="urlImages + starWarsDetails.poster_path" 
                :alt="starWarsDetails.original_title">
                <div v-else>
                    <img
                    src="https://media.istockphoto.com/vectors/error-page-or-file-not-found-icon-vector-id924949200?k=20&m=924949200&s=170667a&w=0&h=-g01ME1udkojlHCZeoa1UnMkWZZppdIFHEKk6wMvxrs=" 
                    alt="image not found">
                    <div
                    class="titolo-image"
                    > 
                        {{starWarsDetails.title}}
                    </div>
                </div>
            </li>
        </ul>
        <!-- Informazioni del film -->
        <ul class="back">  
            <!-- Titolo -->
            <li>
                <span class="bold">Titolo:</span>
                {{starWarsDetails.title}}
            </li>
            <!-- Titolo originale -->
            <li
            >
                <span class="bold">Titolo originale:</span>
                {{starWarsDetails.original_title}}
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
            <li v-if="starWarsDetails.overview">
                <span class="bold">Overview:</span>
                {{starWarsDetails.overview}}
            </li>
            <li v-else>
                <span class="bold">
                    Overview:
                </span>
                non disponibile
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: 'StarWars',
        props: {
            starWarsDetails : Object
        },
        data: function(){
            return{
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

                let vote = null;

                if(this.starWarsDetails.vote_average > 8.5){
                    vote = 5
                    return vote;
                } else if (this.starWarsDetails.vote_average > 6.5) {
                    vote = 4
                    return vote;
                } else if (this.starWarsDetails.vote_average > 4.5) {
                    vote = 3
                    return vote;
                } else if (this.starWarsDetails.vote_average > 2.5) {
                    vote = 2
                    return vote;
                } else if (this.starWarsDetails.vote_average > 0.5) {
                    vote = 1
                    return vote;
                }

                return vote;
            },
        },
    }

</script>

<style lang="scss" scoped>
.single-card{
    width: calc((100% / 1) - 20px);
    margin: 10px;
    border: 1px solid white;
    border-radius: 10px;
    text-align: center;
    color: white;
    // padding: 15px;
    flex-shrink: 0;
    cursor: pointer;
    overflow: hidden;

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
        // height: 450px;
        // overflow-y: auto;
    }

    &:hover .front{
        display: none;
    }

    &:hover .back{
        display: block;
    }

    ul{
        list-style-type: none;
        // height: 450px;
        overflow-y: auto;


        li{
            margin-bottom: 10px;
            font-size: 20px;

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
        width: calc((100% / 4) - 20px)
    }
};
@media screen and (min-width: 1200px){
    .single-card{
        width: calc((100% / 6) - 20px)
    }
}
</style>