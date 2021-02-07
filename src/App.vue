<template>
  <div id="app" >
    <h1>Редактор JSON</h1>
    <hr>
    <MainMenu v-bind:buttons="buttons" />
    <Coder v-bind:buttons="buttons"/>
  </div>
</template>

<script>
import Coder from '@/components/Coder'
import MainMenu from '@/components/MainMenu'

export default {
  name: 'App',
  data() {
    return {
      buttons  : {
        autoformation: false
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
