<!--Ana ekranımız.-->
<template>
    <div class="game-area">
        <!--Kart id sini görüp doğru cevapları öğrenmek istiyorsan p tagını aktifleştir -->
        <!--<p>{{ answer }}</p>-->
        <h1 class="title">Frontend Yazılım Dilini Bul</h1>
        <p class="description">Web tasarım olarak da bilinen Frontend terimi, bir web sitesinin etkileşime girildiği ilk alanıdır. Bu alanda kullanılan yazılım dillerinden oyun yaptık. Hadi biraz eğlenelim... </p>
        <div class="container">
            <transition-group name="rotate-all" appear class="card-container">
                <app-card 
                :key="card.id" 
                :class="{'shadow' : selectedCard == card.id}"
                @click.native="selectedCard = card.id"
                v-for="card in cards" 
                :card="card">
            </app-card>
            </transition-group>
        </div>
        <div class="container">
            <transition name="rotate" mode="out-in">
                <component
                    @click.native="showCard(answer)"
                    :card="answer"
                    :is="activeCard"
                ></component>
            </transition>
        </div>

    </div>
</template>

<script>
    import Card from "./Card.vue";
    import DefaultCard from "./DefaultCard.vue";

    export default {
        components : {
            appCard : Card,
            appDefaultCard : DefaultCard
        },
        data(){
            return{
                selectedCard : null,
                answer : {},
                activeCard : "app-default-card" ,
                cards: [
                    {id : 1, component : "app-card", image : "/src/assets/card-1.png"},
                    {id : 2, component : "app-card", image : "/src/assets/card-2.png"},
                    {id : 3, component : "app-card", image : "/src/assets/card-3.webp"},
                    {id : 4, component : "app-card", image : "/src/assets/card-4.png"},
                    {id : 5, component : "app-card", image : "/src/assets/card-5.webp"},
                    {id : 6, component : "app-card", image : "/src/assets/card-6.png"},
                ]
            }
        },
        created(){
            let answer = Math.ceil(Math.random() * this.cards.length);
            this.answer =this.cards[answer-1];
            
        },
        methods : {
            showCard(answer){
                if(this.selectedCard == null) {
                    alert("Bir Kart seçmeniz gerekiyor!");
                }else{
                    this.activeCard = answer.component;
                    setTimeout(() =>{
                        if(answer.id == this.selectedCard){
                            this.$emit("activeComponentEvent", "app-celebrate");
                        } else {
                            this.$emit("activeComponentEvent", "app-failure");
                        }
                    },1000)
                }
            }
        }
    }
</script>

<style scoped>

    .title{
        text-align: center;
        font-family: Georgia, 'Times New Roman', Times, serif;
        color: rgb(23, 23, 23);
        padding-top: 25px;
    }

    .description{
        text-align: center;
        color: black;
        font-family: Georgia, 'Times New Roman', Times, serif;
    }

    .container, .card-container{
        display: flex;
        justify-content: center;
        align-items: center;
        margin-top: 50px;
    }

    .shadow {
        box-shadow: 0px 8px 45px #0f4ff3!important;
        transition: box-shadow 1s;
    }

    /* Kartların Animasyonu için class tanımları*/
    .rotate-all-enter{}
    .rotate-all-enter-active{
        animation: rotate-all ease-in-out 1.5s forwards ;
    }
    .rotate-all-leave{}
    .rotate-all-leave-active{}

    @keyframes rotate-all {
        from {
            transform: rotateY(0);
        }
        to{
            transform: rotateY(720deg);
        }
    }

    /* Kapalı Kartın Animasyon tanımı */
    .rotate-enter{}
    .rotate-enter-active{
        animation: rotate-in 0.5s ease-in-out forwards;
    }
    .rotate-leave{}
    .rotate-leave-active{
        animation: rotate-out 0.5s ease-in-out forwards;

    }

    @keyframes rotate-in {
        from{
            transform: rotateY(90deg);
        }
        to{
            transform: rotateY(0deg);
        }
    }

    @keyframes rotate-out {
        from{
            transform: rotateY(0deg);
        }
        to{
            transform: rotateY(90deg);
        }
    }




    
</style>