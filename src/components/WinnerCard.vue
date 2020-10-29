<!-- 
  Author: Igor Nogueira
  Date: October 28, 2020
  Description: This component displays a winner card showing who won the battle
-->
<template>
    <div id="winner-card">  
        <h1>Congratulations {{winnerData.winner}}! You won the battle having {{winnerData.hp}} HP remaining.</h1>
    </div>
</template>
<script>

    export default {
        name: 'Round',
        props: {
            winnerData: Object //winner data
        }
    }
</script>
<style scoped>
    #winner-card{
        background: linear-gradient(to left,#9EF6B1,#498957);
        border-radius: 10px;
        box-shadow: 0 3px 10px rgba(0,0,0,0.2);
        margin:10px;
        padding: 20px;
        width:70vw;
        text-align: center;
    }
</style>