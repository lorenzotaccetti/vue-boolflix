<template>
    <ul>
        <li>
            Lingua: 
            <img 
            class="flag" 
            :src="require('../assets/img/' + flagArray[activeFlag].flag)" 
            :alt="flagArray[activeFlag].lang"> 
        </li>
        <li>
            Voto:
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
        <li>
            <img 
            :src="urlImages + notFoundImage" 
            :alt="element.original_title">
        </li>
    </ul>
</template>

<script>
    export default {
        name: 'SingleCard',
        props:{
            element: Object,
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
                
                let vote = null;

                if(this.element.vote_average > 8.5){
                    vote = 5
                    return vote;
                } else if (this.element.vote_average > 6.5) {
                    vote = 4
                    return vote;
                } else if (this.element.vote_average > 4.5) {
                    vote = 3
                    return vote;
                } else if (this.element.vote_average > 2.5) {
                    vote = 2
                    return vote;
                } else if (this.element.vote_average > 0.5) {
                    vote = 1
                    return vote;
                }

                return vote;
            },
            notFoundImage: function(){

                // Funzione per impostare un'immagine di base anche a tutti film e serie tv che non hanno copertina

                let replaceImage = this.element.poster_path;
                
                if(this.element.poster_path === null){
                    replaceImage = '/nTQWWH6CFtl37x1nPx8HRwbwvGn.jpg';
                    return replaceImage
                }

                return replaceImage
            }
        },
    }
</script>

<style lang="scss" scoped>
ul{
    list-style-type: none;
}

li{
    margin-bottom: 10px;
    font-size: 20px;
}

.flag{
    width: 25px;
    height: 20px;
    border-radius: 10px;
    vertical-align: middle;
}
</style>