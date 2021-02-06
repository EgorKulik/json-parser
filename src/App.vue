<template>
  <div id="app" >
    <h1>Редактор JSON</h1>
    <hr>
    <MainMenu />
    <Coder 
      v-bind:jsonstr="jsonstr"
      v-bind:jsonerror="jsonerror"
    />
  </div>
</template>

<script>
import Coder from '@/components/Coder'
import MainMenu from '@/components/MainMenu'

export default {
  name: 'App',
  data: {
    
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
