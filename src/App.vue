<template>

  <div class="header" v-show="showHeader">
    <h1 id = "page_name">CARO GAME</h1>
    <div>
      <img alt="Vue logo" src="./assets/logo.png" id = "logo">
    </div>
    <button id="button-start" @click="homeToMenu">
    START GAME
  </button>
  </div>

  <Menu v-if = "showMenu" @closeMenu = "menuToHome" @modeChoice="chooseMode"/>
  <Game v-if = "showGame" :winningValue="winningValue" @gameToMenu="gameToMenu"/>
</template>

<script>

import Menu from "./components/Menu.vue"
import Game from "./components/Game.vue"

export default {
  name: 'App',
  components: {
    Menu, Game
  },
  data(){
    return{
      showMenu: false,
      showHeader: true,
      showGame: false,
      winningValue: null
    }
  },

  methods:{
    gameToMenu(){
      this.showMenu = false
      this.showHeader = true
      this.showGame = false      
    },

    homeToMenu(){
      this.showMenu = true
      this.showHeader = false
      this.showGame = false
    },

    menuToHome(){
      this.showMenu = false
      this.showHeader = true
      this.showGame = false
    },
    chooseMode(winningValue){
      this.showMenu = false
      this.winningValue = winningValue
      this.showHeader = false
      this.showGame = true

      console.log(this.count)
    }

  }
}
</script>

<style>


#app {
  font-family: Arial, Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #EEEEEE;
  background: #212529;
  width: 500px;
  margin: auto;
  height: 95vh;
  border-radius: 10px;

}

.header{
  padding-top: 200px;
  display: block;
}

#logo{
  max-width: 100px;
  max-height: 100px;
  font-weight: 900;
}

#page_name{
  margin : 0px;
  font-size: 4rem;
  color: #5932cd;
}

#button-start{
  width: 40%;
  height: 50px;
  font-size: 1rem;
  border-radius: 10px;
  font-weight: 600;
  background-color: #5932cd ;
  color: #EEEEEE;
  margin-top: 50px
}

#button-start:hover{
    background-color: #7b16fb;
}
</style>
