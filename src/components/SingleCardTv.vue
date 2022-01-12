<template>
     <!-- Single Card -->
    <ul class="single-card">        
        <li>Titolo: {{element.name}}</li>
        <li>Titolo originale: {{element.original_name}}</li>
        <li>Lingua: <img :src="require('../assets/img/' + flagArray[currentActiveFlag].flag)" :alt="flagArray[currentActiveFlag].lang"> </li>
        <!-- <li>Lingua: {{element.original_language}}</li> -->
        <li>Voto: {{element.vote_average}}</li>
    </ul>
</template>

<script>
    export default {
        name: 'SingleCardTv',
        props:{
            element: Object
        },
        data: function(){
            return{
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
                        flag: 'mondo.jpg'
                    },
                ]
            }
        },
        methods: {
        },
        created: function (){
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
            }
        }
    }
</script>

<style lang="scss" scoped>
.single-card{
    width: calc((100% / 5) - 40px);
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

    img{
        width: 25px;
        height: 20px;
        border-radius: 10px;
    }
}    
</style>