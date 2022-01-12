<template>
    <!-- Single Card -->
    <ul class="single-card">        
        <li>
            Titolo: {{element.title}}
        </li>
        <li>
            Titolo originale: {{element.original_title}}
        </li>
        <SingleCard :element="element"/>
    </ul>
</template>

<script>
import SingleCard from './SingleCard.vue'
    export default {
        name: 'SingleCardMovies',
        props: {
            element: Object,
        },
        components:{
            SingleCard
        },
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