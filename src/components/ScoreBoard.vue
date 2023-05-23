<template>
    <section class="score">
      Jogador <span>{{ this.winCount }}</span> x 
     <span>{{ this.loseCount }}</span> Computador
    </section>
</template>

<script>
    export default {
        props:['winCount', 'loseCount']
    }
</script>

<style lang="scss">
section.score {
    border-bottom: 1px solid black;
    padding: 24px;
    font-size: 18px;

    span {
        padding: 8px;
        font-weight: bold;
        border: 1px solid black;
    }
}
</style>