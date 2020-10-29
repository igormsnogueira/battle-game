<!-- 
  Author: Igor Nogueira
  Date: October 28, 2020
  Description: This component displays a player card showing all information about this player
-->
<template>
  <div class="card">
    <h3 class="title">{{player.name}}</h3>
    <p>Initial HP: {{ player.initialHp }}</p>
    <p>Current HP: {{ player.hp }}</p>
    <p>Attack: {{ player.attack }}</p>
  </div>
</template>

<script>
export default {
  name: 'PlayerCard',
  props: {
    player: Object //player data
  }
}
</script>
<style scoped>
.card{
  display:grid;
  width: 30vw;
  grid-template-columns: repeat(4,auto);
  grid-template-rows: repeat(2,auto);
  border: 2px solid black;
  box-shadow: 0 3px 10px rgba(0,0,0,0.2);
  background:linear-gradient(to right, lightgray, #fff);
  margin: 5px;
  padding: 5px;
  border-radius: 10px;
  font-weight:bold;
  justify-content: space-evenly;
  align-content: center;
}
.title{
  grid-column: 1 / 5;
  grid-row: 1 / 2;
  justify-self: center;
  text-shadow:2px 2px white;
  color:darkgreen;
}
</style>
