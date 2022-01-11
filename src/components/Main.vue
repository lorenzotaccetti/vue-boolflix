<template>
    <main>
        <div class="container">
            <ul class="single-card" v-for="(element, index) in details" :key="index">
                <li>Titolo: {{element.title}}</li>
                <li>Titolo originale: {{element.original_title}}</li>
                <li>Lingua: {{element.original_language}}</li>
                <li>Voto: {{element.vote_average}}</li>
            </ul>
        </div>
    </main>
</template>

<script>
export default {
    name: 'Main',
    props: {
        details : Array,
    },


}
</script>

<style scoped lang="scss">
main{
    height: calc(100% - 100px);
    
    .container{
        width: 90%;
        margin: auto;
        display: flex;
        flex-wrap: wrap;

        .single-card{
            width: calc((100% / 5) - 40px);
            margin: 20px;
            list-style-type: none;
            background-color: rgb(133, 80, 80);
            border-radius: 10px;
            text-align: center;
            color: white;
            padding: 10px;

            li{
                margin-bottom: 10px;
            }
        }
    }
}
</style>