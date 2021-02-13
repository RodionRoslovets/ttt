<template>
  <div class="container">
      <cell v-for="n in 9" :key="n" @checkEndGame="checkEndGame($event)">

      </cell>
  </div>
</template>

<script>
import Cell from './Cell'
export default {
    components:{
        Cell
    },
    data(){
        return {
            //выйгрышные комбинации
            winCombinations:[
                [1,2,3],
                [4,5,6],
                [7,8,9],
                [1,4,7],
                [2,5,8],
                [3,6,9],
                [1,5,9],
                [3,5,7]
            ],
            moves:[]
        }
    },
    methods:{
        clearField(){
            this.$children.forEach(cell => cell.$el.innerHTML = '')
        },
        checkEndGame(role){
            this.moves.push(role)
            let player = [],
                ai = [],
                isGameEnd = false,
                isPlayerWin = false,
                isAiWin = false

            this.$children.forEach((cell,index)=>{
                if(cell.$el.innerHTML === 'X'){
                    player.push(index + 1)
                } else if(cell.$el.innerHTML === 'O') {
                    ai.push(index + 1)
                }
            })

            this.winCombinations.forEach(combination => {
                if(player.filter((elem)=>{return combination.indexOf(elem) !== -1}).length == 3){
                    isPlayerWin = true
                }
            })

            this.winCombinations.forEach(combination => {
                if(ai.filter((elem)=>{return combination.indexOf(elem) !== -1}).length == 3){
                    isAiWin = true
                }
            })

            if(isPlayerWin || isAiWin) {
                isGameEnd = true
            }

            if(isGameEnd || this.$children.filter(cell => cell.$el.innerHTML === '').length === 0){
                console.log(`Game over, ${this.moves[this.moves.length - 1]} wins`)
                this.moves = []
                this.clearField()
            } else if(this.moves[this.moves.length - 1] === 'player'){
                this.aiMove()
            }
        },
        //ход ии
        aiMove(){
            let randIndex = Math.floor(Math.random() * 9)

            if(this.$children[randIndex].$el.innerHTML === ''){
                this.$children[randIndex].$el.innerHTML = 'O'
            } else {
                this.aiMove()
            }

            this.checkEndGame('ai')
        }
    }
}
</script>

<style>

.container{
    width: 300px;
    height: 300px;
    display:flex;
    flex-wrap: wrap;
}

</style>