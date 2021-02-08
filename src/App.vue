<template>
  <div id="app" >
    <h1>Редактор JSON</h1>
    <hr>
    <MainMenu v-bind:controller="controller" />
    <Coder v-bind:controller="controller"/>
  </div>
</template>

<script>
import Coder from '@/components/Coder'
import MainMenu from '@/components/MainMenu'

export default {
  name: 'App',
  data() {
    return {
      controller  : {
        autoformation: false,
        stringlog: [],
        jsonstr: "",
        iterator: 0
      }
    }
  }, 
  components: {
    Coder,
    MainMenu
  }
}
</script>

<style>
.text{
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
