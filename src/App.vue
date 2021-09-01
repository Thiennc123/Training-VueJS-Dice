<template>
    <div id="app">
        <div class="wrapper clearfix"> 
            <PlayerComponent 
                v-bind:isWiner="isWiner"
                v-bind:scorePlayer ="scorePlayer"
                v-bind:currentScore ="currentScore"
                v-bind:activePlayer ="activePlayer"
            />
            <ControlComponent
                v-bind:scoreWiner="scoreWiner"
                v-bind:isPlaying="isPlaying"
                @handleChangeScoreWiner="handleChangeScoreWiner"
                @handleNewGame="handleNewGame"
                @handleRollDice="handleRollDice"
                @handleHoldScore="handleHoldScore"
            />
            <DiceComponent
                v-bind:dices="dices"
            /> 
        </div>
    </div>
</template>

<script>
import PlayerComponent from './components/Players.vue';
import ControlComponent from './components/Controls.vue';
import DiceComponent from './components/Dices.vue';
export default {
    name: 'App',
    data(){
        return{
            isPlaying: false,
            activePlayer:0,
            scorePlayer:[0,0],
            currentScore: 0,
            dices:[1, 1],
            scoreWiner:10,
        }
    },
    components: {
        PlayerComponent,
        ControlComponent,
        DiceComponent,
    },
    computed:{
        isWiner(){
            let{scorePlayer, scoreWiner} = this;
            if((scorePlayer[0] >= scoreWiner) || (scorePlayer[1] >= scoreWiner)){
                return true;
            }
            return false;
        }
    },
    methods: {
        handleNewGame() {
            this.isPlaying = true;
            this.activePlayer = 0;
            this.scorePlayer = [0, 0];
            this.currentScore = 0;
            this.dices = [1,1];
        },
        handleRollDice() {
            if(this.isPlaying){
                var dice1 = Math.floor(Math.random() * 6) + 1;
                var dice2 = Math.floor(Math.random() * 6) + 1;
                this.dices = [dice1, dice2];
                if(dice1 == 1 || dice2 == 1){
                    setTimeout( () => {
                        alert("So bad!!!"); 
                    }, 10);
                    this.activePlayer = this.activePlayer == 0? 1: 0;
                    this.currentScore = 0;
                }else{
                    this.currentScore += dice1 + dice2;
                }
            }else{
                alert("Please choose New Game");
            }
        },  
        handleHoldScore() {
            let {scorePlayer, activePlayer, currentScore} = this;
            let scoreOld = scorePlayer[activePlayer];
            this.$set(this.scorePlayer, activePlayer, scoreOld+currentScore);
            if(!this.isWiner){
                this.activePlayer = activePlayer == 0? 1: 0;
                this.currentScore = 0;
            }else{
                this.isPlaying = false;
            }
        },
        handleChangeScoreWiner(e) {
            var number = parseInt(e.target.value);
            if(isNaN(number)){
                this.scoreWiner = '';
            }else{
                this.scoreWiner = number;
            }
        }
    },
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    
}

.clearfix::after {
    content: "";
    display: table;
    clear: both;
}

body {
    background-image: linear-gradient(rgba(62, 20, 20, 0.4), rgba(62, 20, 20, 0.4)), url('/asset/back.jpg');
    background-size: cover;
    background-position: center;
    font-family: Lato;
    font-weight: 300;
    position: relative;
    height: 100vh;
    color: #555;
}

.wrapper {
    width: 1000px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
    box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
    overflow: hidden;
}
</style>
