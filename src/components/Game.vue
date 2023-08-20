<template>
    <button class="game-header" @click="gameToMenu">
    <i class="fa-solid fa-house"></i>
    <div>HOME</div>
    </button>

    <div class = "board-game" id = "board-game">
        <div v-for="n in rows" :key="n" class = "board">
            <button v-for="m in numbers" :key="m" class="cell" @click="changeTurn" :id="`${n}.${m}`" :disabled="isActive">
            </button>
        </div>
    </div>

    <p class="result" v-if = "showResult">The winner is <span style="font-family : 'Finger Paint'; font-size = '2rem'">{{ winner }}</span></p>


</template>

<script>
export default {


    props:['winningValue'],
    data(){
        return {
        rows: 10,
        numbers: 10,
        board: Array(10).fill().map(() => {return Array(10).fill(null)}),
        currentPlayer: "x",
        winner: null,
        showResult: false,
        isActive: false 
        }
    },

    methods: {

        gameToMenu(){
            this.winner = null
            this.currentPlayer = "x"
            this.isActive = false
            this.board = Array(10).fill().map(() => {return Array(10).fill(null)})
            this.$emit("gameToMenu")
        },

        endGame(){
            this.winner = this.currentPlayer
            this.showResult = true
            this.board = Array(10).fill().map(() => {return Array(10).fill(null)})
            this.isActive = true
        },
        changeTurn(e){

            //get long, lat from cellID
            var cellID = e.srcElement.id
            var row = Number(e.srcElement.id.split(".")[0])-1
            var col = Number(e.srcElement.id.split(".")[1])-1     
            
            if(!this.board[row][col]){

                //
                this.board[row][col] = this.currentPlayer
                e.target.innerText = this.currentPlayer
     
            


                //check winning in a row
                var count = 1
                var leftCol = col -1
                while (leftCol >= 0 && this.board[row][leftCol] == this.currentPlayer){
                    count++
                    leftCol--
                }

                var rightCol = col + 1;

                while (rightCol <= 9 && this.board[row][rightCol] == this.currentPlayer){
                    count++
                    rightCol++
                }

                console.log(`${this.currentPlayer} : ${count}`)

                if(count >= this.winningValue){
                    this.endGame()
                }


                //check winning in a column
                count = 1
                var upperRow = row + 1

                while (upperRow <= 9 && this.board[upperRow][col] == this.currentPlayer){
                    count++
                    upperRow++

                }

                var lowerRow = row - 1
                while (lowerRow >= 0 && this.board[lowerRow][col] == this.currentPlayer){
                    count++
                    lowerRow--
                }

                if(count >= this.winningValue){
                    this.endGame()

                }

                console.log(`${this.currentPlayer} : ${count}`)

                //check winning in a diagonal
                count = 1

                upperRow = row + 1
                rightCol = col + 1
                while(upperRow <= 9 && rightCol <= 9 && this.board[upperRow][rightCol] == this.currentPlayer){
                    console.log(`diagonal: ${this.board[upperRow][rightCol]}`)
                    
                    count++
                    upperRow++
                    rightCol++
                    
                }

                lowerRow = row - 1
                leftCol = col - 1
                while(lowerRow >=0 && leftCol >= 0 && this.board[lowerRow][leftCol] == this.currentPlayer){
                    console.log(`diagonal: ${this.board[lowerRow][leftCol]}`)

                    
                    count++
                    leftCol--
                    lowerRow--
                }

                console.log(`${this.currentPlayer} : ${count}`)

                if(count >= this.winningValue){
                    this.endGame()

                }
                //another possibility in diagonal
                count = 1

                leftCol = col - 1
                upperRow = row + 1
                while(upperRow <= 9 && leftCol >= 0 && this.board[upperRow][leftCol] == this.currentPlayer){
                    
                    console.log(this.board[upperRow][rightCol])
                    count++
                    upperRow++
                    leftCol--
                }

                rightCol = col + 1
                lowerRow = row - 1
                while(lowerRow >= 0 && rightCol <= 9 && this.board[lowerRow][rightCol] == this.currentPlayer){
                    
                    console.log(this.board[lowerRow][rightCol])
                    count++
                    lowerRow--
                    rightCol++
                }
                
                console.log(`${this.currentPlayer} : ${count}`)

                if(count >= this.winningValue){
                    this.endGame()
                }

                //change turn
                this.currentPlayer =   this.currentPlayer == "x"? "o" :"x"  
            }
        }


    }
    }
</script>

<style>

.game-header{
    display: flex;
    padding: 10px;
    font-size: 1rem;
    gap:10px;
    background-color: #5932cd ;
    color: #EEEEEE;
    border-radius: 10px;
    font-weight: 600;
    margin-bottom: 50px;
}

.game-header:hover{
    background-color: #7b16fb;
}

.result{
    background-color: #5932cd ;
    color: #EEEEEE;
    border-radius: 10px;
    font-weight: 600;    
    width:400px;
    height: 50px;
    margin: 50px;
    text-align: center;
    display: flex;
    flex-direction: column;
    align-content: center;
    justify-content: center;

}





.board{
 
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-content: center;

}

.cell{
    border: 1px solid white;
    width: 40px;
    height: 40px;
    background-color: #5932cd;
    padding: 0px 0px;
    font-family: "Finger Paint";
    font-size: 25px;
    text-align: center;
    color: white;
    
  }

.cell:hover{
        background-color: #7b16fb;
}

</style>