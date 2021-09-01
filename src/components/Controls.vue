<template>
  <div class="wrapper-controls">
        <button 
            @click="newGame"
            class="control btn-new"><i class="ion-ios-plus-outline"
        ></i>New game</button>
        <button 
            @click="rollDice"
            class="control btn-roll"><i class="ion-ios-loop"
        ></i>Roll dice</button>
        <button 
            @click="holdScore"
            class="control btn-hold"><i class="ion-ios-download-outline"
            ></i>Hold</button>
        <input v-bind:value="scoreWiner" @input="handleInput" type="number" placeholder="Final score" class="final-score" v-bind:disabled="isPlaying">
  </div>
</template>

<script>
export default {
    name: 'ControlComponent',
    data(){
        return {
           
        }
    },
    props: {
        scoreWiner:{ type: [Number, String], default: () => 100},
        isPlaying:{ type: Boolean, default: () => false},

    },
    methods:{
        newGame(){
            this.$emit("handleNewGame");
        },
        rollDice(){
            this.$emit("handleRollDice")
        },
        holdScore() {
            this.$emit("handleHoldScore");
        },
        handleInput(e){
            this.$emit('handleChangeScoreWiner',e);
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

</style>
