<!-- 
  Author: Igor Nogueira
  Date: October 28, 2020
  Description: This is the main component of the battle game where we will build the main structure and manipulate the app data/state
-->
<template>
  <div id="app">
    <!-- button to restart the round using the same players -->
    <button v-on:click="restart">Restart</button>
    <!-- Component to show the player cards in the battle  -->
    <Battle v-bind:player1="player1" v-bind:player2="player2"/>
    <!-- Here we use a loop to display data about each round that will happen in a 2.5 seconds interval  -->
    <div id="rounds-wrapper">
      <Round v-for="round in rounds" :key="round.roundNumber" v-bind:roundData="round" />
    </div>
    <!-- Component to show the battle winner -->
    <WinnerCard v-if="finished" v-bind:winnerData="winnerData"/>
  </div>
</template>

<script>
import Round from './components/Round.vue';
import WinnerCard from './components/WinnerCard.vue';
import Battle from './components/Battle.vue';

/*
  This class describes a player and it is used to create the two players that will batle in this game.
*/
class Player{
  /* 
    constructor method to initiate the attribute values for a new player. initial hp is a random number from 50 to 100 and attack is a random number from 5 to 10
  */
  constructor(name){
    this.name = name;
    this.initialHp = Math.round((Math.random()*(100-50)) + 50);//it will create a random number between 50 and 100 for the hp
    this.hp = this.initialHp;
    this.attack = Math.round((Math.random()*(10-5)) + 5); //it will create a random number between 5 and 10 for the attack
  }
  /* Method to attack, it calculates a random number between -10 and 10 and sum it to this current player attack strength
     return: the damage caused by this attack
  */
  attacking(){
    const currentAttack = this.attack + Math.round((Math.random() * (10+10) - 10)); // to get a random value in a range (random from 0 to 1) * range + lowest value
    return currentAttack;
  }
  /* 
    This method is used to deffend by reducing the player hp subtracting the damage suffered from an attack 
    params: attack -> it is the value to be reduced in the player HP, it is related to the damage suffered in the round
  */
  deffend(attack){
    const newHp = this.hp - attack;
    //after reducing the hp, if it is less than zero it does not makes sense as the player is dead, so, we set it to zero instead
    if(newHp >= 0)
      this.hp = newHp;
    else
      this.hp = 0;
  }
}
//Creating the two players that will battle in the game
const firstPlayer = new Player("Player 1");
const secondPlayer = new Player("Player 2");

export default {
  name: 'App',
  components: {
    Round,
    WinnerCard,
    Battle
  },
  data(){
    return {
      player1: firstPlayer, //first player created
      player2: secondPlayer, //second player created
      //initialFirstPlayerLife : 0, //variable that
      //initialSecondPlayerLife : 0,
      roundNumber: 0,
      rounds: [],
      finished: false,
      winnerData: {}
    }
  },
  //Method executed when this component is mounted in the DOMm it will run the first round
  mounted(){
    this.runRound();
  },
  //Method executed when this component is update(some state/data changes) it will run one round after waiting 2.5s
  updated(){
    setTimeout(()=>this.runRound(),2500);
  },
  methods: {
    /*
      This method executes a new round in the battle, allowing the player with less hp to attack first and then the player with more hp to attack later
      It updates the round number and add the information of the current round to the round array data
    */
    runRound(){
      const player1 = this.player1;
      const player2 = this.player2;
      //if both are still alive, we will create a new round
      if(player1.hp > 0 && player2.hp > 0){
        this.roundNumber++; //increasing round number
        let damage1,damage2;
        //the player with less hp attacks first
        if(player1.hp < player2.hp){
          damage1 = player1.attacking(); //player 1 attacking first
          damage2 = player2.attacking(); //player 2 attacking
          //pushing a new roung in the round array with all information of this round
          this.rounds.push({roundNumber:this.roundNumber,player1Hp: player1.hp, player2Hp: player2.hp, damagePlayer1:damage2,damagePlayer2:damage1,firstAttacker:"Player 1",secondAttacker:"Player 2"});
          //updating players hp by reducing the damage suffered using the deffend method
          player1.deffend(damage2);
          player2.deffend(damage1);
        }else{
          damage1 = player2.attacking();
          damage2 = player1.attacking();
          this.rounds.push({roundNumber:this.roundNumber,player1Hp: player1.hp, player2Hp: player2.hp,damagePlayer1:damage1,damagePlayer2:damage2,firstAttacker:"Player 2",secondAttacker:"Player 1"});
          player1.deffend(damage1);
          player2.deffend(damage2);
        }
        
      }else{
        //case someone died we set up winner data
        this.winnerData.winner = (player1.hp > 0) ? "Player 1": "Player 2"; //the winner is the one whose hp is still higher than 0
        this.winnerData.hp = (player1.hp > 0) ? player1.hp : player2.hp;
        this.finished = true;
      }                     
    },
    // Method executed when the restart button is clicked, it restarts the data to their initial state and reset the players hp to their initial value generated when the game was opened
    restart(){
      this.player1.hp = this.player1.initialHp;
      this.player2.hp = this.player2.initialHp;
      this.roundNumber = 0;
      this.rounds = [];
      this.finished = false;
      this.winnerData = {};
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Lato:wght@300&display=swap');
#app{
  display: flex;
  flex-direction: column;
  align-items: center;
}
*{
   box-sizing: border-box;
   font-family: 'Lato', sans-serif;
   color: #333;
   line-height: 1.6;
}
#rounds-wrapper{
  display:flex;
  flex-wrap:wrap;
}
#app button{
  align-self: flex-end;
  padding: 5px;
  border-radius: 5px;
  font-weight:bold;
}
#app button:hover{
  background-color:darkgrey;
}
</style>
