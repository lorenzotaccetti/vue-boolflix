<template>
    <!-- Single Card -->
    <ul class="single-card">        
        <li>
            Titolo: {{element.name}}
        </li>
        <li>
            Titolo originale: {{element.original_name}}
        </li>
        <SingleCard :element="element" />
    </ul>
</template>

<script>
import SingleCard from './SingleCard.vue';
    export default {
        name: 'SingleCardTv',
        components: {
            SingleCard
        },
        props:{
            element: Object
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
}    
</style>