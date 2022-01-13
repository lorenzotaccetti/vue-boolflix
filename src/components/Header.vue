<template>
    <header>
        <!-- Logo -->
        <div class="logo">
            <img src="../assets/img/netflixlogo.png" alt="logo Netflix">
        </div>
        <!-- Input -->
        <input 
        v-model="researchText" 
        type="text" 
        placeholder="Cerca un film o una serie tv">
        <!-- Bottone -->
        <button 
        @click="$emit('searchClicked', researchText)">
            Cerca
        </button>
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
    height: 105px;
    line-height: 100px;
    background-color: black;
    display: flex;
    align-items: center;
    border-bottom: 1px solid #e20a13;

    .logo{
        flex-grow: 1;
        margin-left: 30px;
        display: none;

        img{ 
            vertical-align: middle;
            width: 200px;
            height: 100px;
        }
    }

    @media screen and (min-width: 700px) {
        .logo{
            display: inline-block;
        }
    }

    input{
        margin-left: 30px;
        margin-right: 30px;
        padding: 5px 20px;
        min-width: 350px;
        min-height: 30px;
        border-radius: 10px;
        text-align: center;
        border: 1px solid white;
        background-color: lightgrey;
        font-size: 20px;
    }

    button{
        padding: 5px 20px;
        margin-right: 20px;
        border-radius: 10px;
        border: 1px solid white;
        background-color: lightgrey;
        cursor: pointer;
        font-size: 20px;
    }
}
</style>