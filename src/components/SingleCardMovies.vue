<template>
    <!-- Single Card -->
    <ul class="single-card">        
        <li>
            Titolo: {{element.title}}
        </li>
        <li>
            Titolo originale: {{element.original_title}}
        </li>
        <li>
            Lingua: 
            <img 
            class="flag" 
            :src="require('../assets/img/' + flagArray[currentActiveFlag].flag)" 
            :alt="flagArray[currentActiveFlag].lang"> 
        </li>
        <li>
            Voto:
            <i 
            v-for="(element, index) in (0 + vote)" 
            :key="index" 
            class="fas fa-star">
            </i>
            <i 
            v-for="(element, index) in (5 - vote)" 
            :key="index" 
            class="far fa-star">
            </i>
        </li>
        <li>
            <img 
            :src="urlImages + element.poster_path" 
            :alt="element.original_title">
        </li>
    </ul>
</template>

<script>
    export default {
        name: 'SingleCard',
        props: {
            element: Object
        },
        data: function(){
            return{
                vote: null,
                urlImages: 'https://image.tmdb.org/t/p/w342', 
                currentActiveFlag: null,
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
        },
        created: function (){

            // Funzione per determinare quale bandiera mettere per la lingua
            if (this.element.original_language === 'it'){
                this.currentActiveFlag = 0;
            } else if (this.element.original_language === 'en'){
                this.currentActiveFlag = 1
            } else if (this.element.original_language === 'es'){
                this.currentActiveFlag = 2
            } else if (this.element.original_language === 'fr'){
                this.currentActiveFlag = 3
            } else {
                this.currentActiveFlag = 4
            };

            // Funzione per determinare il voto tramite stelle
            if(this.element.vote_average > 8.5){
                this.vote = 5
            } else if (this.element.vote_average > 6.5) {
                this.vote = 4
            } else if (this.element.vote_average > 4.5) {
                this.vote = 3
            } else if (this.element.vote_average > 2.5) {
                this.vote = 2
            } else if (this.element.vote_average > 0) {
                this.vote = 1
            } else{
                this.vote = null
            }
        }
    }
</script>

<style lang="scss" scoped>
.single-card{
    width: calc((100% / 3) - 40px);
    margin: 20px;
    list-style-type: none;
    border: 1px solid black;
    border-radius: 10px;
    text-align: center;
    color: black;
    padding: 15px;

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
}
</style>