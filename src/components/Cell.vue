<template>
  <div class="cell"
    @click="makeMove('player', $event)"></div>
</template>

<script>
export default {
    data(){
        return {

        }
    },
    methods:{
        //ход игрока
        makeMove(player, e){
            if(player === 'player' && e.target.innerHTML === "" ){
                e.target.innerHTML = "X"

                this.$emit('checkEndGame', 'player')
            } 
        }
    }
}
</script>

<style>
    .cell{
        width: 100px;
        height: 100px;
        border:1px solid black;
        box-sizing: border-box;
        text-align: center;
        font-size: 24px;
        line-height: 100px;
    }
    .cell:hover{
        background:#ececec;
        cursor:pointer;
    }
</style>