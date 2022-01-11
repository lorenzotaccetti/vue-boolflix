<template>
    <header>
        <input v-model="researchText" type="text" placeholder="Cerca un film o una serie tv">
        <button @click="$emit('searchClicked', researchText)">Cerca</button>
    </header>
</template>

<script>
export default {
    name: 'Header',
    data: function(){
        return{
            researchText: '',
        }
    }

}
</script>

<style scoped lang="scss">
header{
    padding: 40px;
    background-color: rgba(191, 182, 182, 0.831);

    input{
        margin-right: 30px;
        padding: 5px 20px;
        min-width: 250px;
        border-radius: 10px;
        text-align: center;
        border: 1px solid black;
    }

    button{
        padding: 5px 20px;
        border-radius: 10px;
        border: 1px solid black;
        cursor: pointer;
    }
}
</style>