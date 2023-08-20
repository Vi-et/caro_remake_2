<template>

    <button class="menu-header" @click="menuBackToHome">
        <i class="fa-solid fa-house"></i>
        <div>HOME</div>
    </button>

    <div class="selection">
        <p id = "selection-title">SELECT GAME MODE</p>
        <button class="choice" @click = "modeSelection">3x3</button>
        <button class="choice" @click = "modeSelection">4x4</button>
        <button class="choice" @click = "modeSelection">5x5</button>
    </div>
</template>

<script>
export default {
    methods :{
        menuBackToHome(){
            this.$emit('closeMenu')
        },

        modeSelection(e){
            console.log(e)
            const winningValue = e.srcElement.innerText[0]
          
            this.$emit("modeChoice", winningValue)
        }
    }
}
</script>

<style>

.menu-header{
    display: flex;
    padding: 10px;
    font-size: 1rem;
    gap:10px;
    background-color: #5932cd ;
    color: #EEEEEE;
    border-radius: 10px;
    font-weight: 600;
}

.menu-header:hover{
    background-color: #7b16fb;
}

.selection{
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;

    margin: auto;
    gap: 30px;
    text-align: center;
    padding-top: 200px

}

#selection-title{
    font-size: 2rem;
}

.choice{
    height: 50px;
    border-radius: 10px;
    width: 200px;
    font-size: 2rem;
    background-color: #5932cd ;
    color: #EEEEEE;
    font-weight: 600;

}

.choice:hover{
        background-color: #7b16fb;
}
</style>