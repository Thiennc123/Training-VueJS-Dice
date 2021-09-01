<template>
  <div class="wrapper-players">
    <div class="player-panel" v-bind:class="{ active: activePlayer == 0 }">
        <div class="player-name">{{getName(0)}}</div>
        <div class="player-score">{{scorePlayer[0]}}</div>
        <div class="player-current-box">
            <div class="player-current-label">Current</div>
            <div class="player-current-score">{{activePlayer == 0? currentScore: 0}}</div>
        </div>
    </div>
    
    <div class="player-panel" v-bind:class="{ active: activePlayer == 1 }">
        <div class="player-name">{{getName(1)}}</div>
        <div class="player-score">{{scorePlayer[1]}}</div>
        <div class="player-current-box">
            <div class="player-current-label">Current</div>
            <div class="player-current-score">{{activePlayer == 1? currentScore: 0}}</div>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PlayerComponent',
  props: {
    scorePlayer:{ type: Array, default: () => [0, 0]},
    currentScore:{ type: Number, default: () => 0},
    activePlayer:{ type: Number, default: () => 0},
    isWiner:{type: Boolean, default: () => false},
  },
  methods: {
      getName(index){
          var name = 'Player' + (index + 1);
            console.log(this.activePlayer, this.isWiner, index);
          if(this.activePlayer == index && this.isWiner){
              name = 'Winner';
          }

          return name;
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
    .player-panel {
    width: 50%;
    float: left;
    height: 600px;
    padding: 100px;
    transition: all .3s ease;
    background-color: #fff;
}
.player-name {
    font-size: 40px;
    text-align: center;
    text-transform: uppercase;
    letter-spacing: 2px;
    font-weight: 100;
    margin-top: 20px;
    margin-bottom: 10px;
    position: relative;
}

.player-score {
    text-align: center;
    font-size: 80px;
    font-weight: 100;
    color: #42b983;
    margin-bottom: 130px;
}

.active { background-color: #f7f7f7; }
.active .player-name { font-weight: 300; }

.active .player-name::after {
    content: "\2022";
    font-size: 47px;
    position: absolute;
    color: #42b983;
    top: -7px;
    right: 10px;
    
}

.player-current-box {
    background-color: #42b983;
    color: #fff;
    width: 40%;
    margin: 0 auto;
    padding: 12px;
    text-align: center;
}

.player-current-label {
    text-transform: uppercase;
    margin-bottom: 10px;
    font-size: 12px;
    color: #222;
}

.player-current-score {
    font-size: 30px;
}

.winner { background-color: #f7f7f7; }
.winner .player-name { font-weight: 300; color: #42b983; }
.control {
    position: absolute;
    width: 200px;
    left: 50%;
    transform: translateX(-50%);
    color: #555;
    background: none;
    border: none;
    font-family: Lato;
    font-size: 20px;
    text-transform: uppercase;
    cursor: pointer;
    font-weight: 300;
    transition: background-color 0.3s, color 0.3s;
}
.control.disable {
    pointer-events: none;
}

.control:hover { font-weight: 600; }
.control:hover i { margin-right: 20px; }

.control:focus {
    outline: none;
}

.control i {
    color: #42b983;
    display: inline-block;
    margin-right: 15px;
    font-size: 32px;
    line-height: 1;
    vertical-align: text-top;
    margin-top: -4px;
    transition: margin 0.3s;
}

.btn-new { top: 45px;}
.btn-roll { top: 403px;}
.btn-hold { top: 467px;}

.final-score {
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    top: 520px;
    color: #555;
    font-size: 18px;
    font-family: 'Lato';
    text-align: center;
    padding: 10px;
    width: 160px;
    text-transform: uppercase;
}

.final-score:focus { outline: none; }
</style>
