<template>
    <header>
        <!-- Logo -->
        <div class="logo">
            <img src="../assets/img/netflixlogo.png" alt="logo Netflix">
        </div>
        <!-- Header Nav -->
        <div>
            <div class="nav">
                <div class="nav-element">
                    Home
                </div>
                <div class="nav-element">
                    Serie Tv
                </div>
                <div class="nav-element">
                    Film
                </div>
                <div class="nav-element">
                    Originali
                </div>
            </div>
        </div>
        <div
        class="search-area">
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
        </div>
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
    justify-content: space-between;
    border-bottom: 1px solid #e20a13;

    .logo{
        flex-grow: 0;
        margin-left: 30px;
        display: none;
        cursor: pointer;

        img{ 
            vertical-align: middle;
            width: 200px;
            height: 100px;
        }
    }

    @media screen and (min-width: 780px) {
        .logo{
            display: inline-block;
        }
    }

    .nav{
        display: none;
        justify-content: space-between;
        color: white;

        .nav-element{
            margin: 0 20px;
            font-size: 20px;
            font-weight: bold;
            cursor: pointer;

            &:hover{
                text-decoration: underline;
            }
        }
    }

    @media screen and (min-width: 1200px) {
        .nav{
            display: flex;
        }
    }

    .search-area{
        display: flex;

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
}
</style>