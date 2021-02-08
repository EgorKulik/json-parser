<template>
  <div id="app" >
    <h1>Редактор JSON</h1>
    <hr>
    <MainMenu v-bind:controller="controller" @save-file="saveFile()" />
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
  },
  methods: {
    saveFile: function() {
      if(this.controller.jsonstr == "")
        return;
      const blob = new Blob([this.controller.jsonstr], {type: 'text/plain'})
      const e = document.createEvent('MouseEvents'),
      a = document.createElement('a');
      a.download = "test.txt";
      a.href = window.URL.createObjectURL(blob);
      a.dataset.downloadurl = ['text/json', a.download, a.href].join(':');
      e.initEvent('click', true, false, window, 0, 0, 0, 0, 0, false, false, false, false, 0, null);
      a.dispatchEvent(e);
    },
    onKeyDown(event) {
      if (navigator.platform === "MacIntel" ? event.metaKey : event.ctrlKey && event.key === "s") {
        event.preventDefault()

        this.saveFile();
      }
    }
  },
  created() {
    document.addEventListener('keydown', this.onKeyDown);
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
