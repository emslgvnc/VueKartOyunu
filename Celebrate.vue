<!--Doğru cevap verdiğimizde karşımıza çıkacak ekran-->
<template>
    <div class="container">
        <h1>Tebrikler... Bildiniz!!!</h1>
        <button @click="newGame">Yeni Oyun</button>
    </div>
</template>

<script>
    export default{
        methods : {
            newGame(){
                this.$emit("activeComponentEvent", "app-game-cards")
            }
        }
    }
</script>

<style scoped>
    .container{
        position: absolute;
        top: 0px;
        left: 0px;
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        background-color: #1874cd;
    }
    
    .container h1{
        text-align: center;
        font-size: 250%;
        color: aliceblue;
        font-family: Georgia, 'Times New Roman', Times, serif;
    }

    .container button{
        cursor: pointer;
        width: 200px;
        height: 50px;
        background-color: aliceblue;
        color: #1c0f45;
        border: 2px solid #1c0f45;
        font-size: 20px;
        border-radius: 10px;
        transition: .5s;
    }

    .container button:hover{
        background-color:  #87ceff;
        color:  #1c0f45;
        transition: .5s;
    }
</style>