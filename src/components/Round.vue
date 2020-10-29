<!-- 
  Author: Igor Nogueira
  Date: October 28, 2020
  Description: This component displays all the information about each round
-->
<template>
    <div id="round-wrapper">
        <!-- showing round number -->
        <b>Round {{roundData.roundNumber}}</b>  
        <!-- showing current player 1 hp before the attacks  -->
        <p>Player 1 HP: {{roundData.player1Hp}}</p>
        <!-- showing current player 2 hp before the attacks  -->
        <p>Player 2 HP: {{roundData.player2Hp}}</p>
        <!-- showing who attacks first  -->
        <p>{{roundData.firstAttacker}} Attacking First ...</p>
        <!-- showing the damage caused by the player that attacked first based on the condition-->
        <p class="damage" v-if="roundData.firstAttacker == 'Player 1'">Damage Cause By Player 1: {{roundData.damagePlayer2}}</p>
        <p class="damage" v-else>Damage Cause By Player 2: {{roundData.damagePlayer1}}</p>
        <!-- showing who attacks after  -->
        <p>{{roundData.secondAttacker}} Attacking Now ...</p>
          <!-- showing the damage caused by the player that attacked second based on the condition-->
        <p class="damage" v-if="roundData.secondAttacker == 'Player 1'">Damage Cause By Player 1: {{roundData.damagePlayer2}}</p>
        <p  class="damage" v-else>Damage Cause By Player 2: {{roundData.damagePlayer1}}</p>
    </div>
</template>
<script>
    export default {
        name: 'Round',
        props: {
            roundData: Object //all data about this round
        }
    }
</script>
<style scoped>
    #round-wrapper{
        background: #fff;
        border-radius: 10px;
        box-shadow: 0 3px 10px rgba(0,0,0,0.2);
        margin:10px;
        padding: 20px;
        width:22vw;
    }
    .damage{
        color: red;
        font-weight: bold;
    }
</style>