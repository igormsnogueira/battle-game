<!-- 
  Author: Igor Nogueira
  Date: October 28, 2020
  Description: This is a battle component to display the current battle showing the two player cards with their information 
-->
<template>
    <div id="battle">  
        <!-- Display both player cards and a VS (versus) image in the middle of the player cards to demonstrate that it is a battle -->
        <PlayerCard v-bind:player="player1" />
        <img id="vs" src="../assets/vs.png">
        <PlayerCard v-bind:player="player2" />
    </div>
</template>
<script>
    import PlayerCard from "./PlayerCard";
    export default {
        name: 'Battle',
        components: {
            PlayerCard
        },
        props: {
           player1: Object, //player 1 information
           player2: Object //player 2 information
        }
    }
</script>
<style scoped>
    #battle{
        display: flex;
        justify-content: center;
    }
    #vs{
        height:27vh;
        width:13vw;
    }
</style>