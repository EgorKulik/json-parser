<template>
  <div id="app" >
    <h1>Редактор JSON</h1>
    <hr>
    <MainMenu v-bind:controller="controller" @save-file="saveFile()" @hightlight-text="hightLightText()" @make-folding="makeFolding()"/>
    <Coder v-bind:controller="controller" @hightlight-text="hightLightText()" @make-folding="makeFolding()"/>
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
        iterator: -1,
        jsonhtml: "",
        foldingmas: [],
        jsoncorrect: false,
        foldedstrs: []
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
    },
    hightLightText: function(){
        this.controller.jsonhtml = this.controller.jsonstr.replace(/"(\w*|\s*|\d*)*"/gi, str => "<span style=\"color: red;\">" + str + "</span>");
    },
    makeFolding: function(){
        this.controller.foldingmas = [];
        if(this.controller.iterator == -1 || this.controller.jsoncorrect == false)
          return;
        var rows = this.controller.jsonstr.split("\n");
        rows.forEach((element, index) => {
            if(element.match(/{|\[/))
            {
                if(this.controller.foldedstrs[index] == undefined)
                  this.controller.foldingmas.push("v");
                else
                  this.controller.foldingmas.push(">");
            }
            else
                this.controller.foldingmas.push(" ");
        });
    }
  },
  created() {
    document.addEventListener('keydown', this.onKeyDown);
  },
  mounted() {
    window.onload = () =>{
      this.controller.jsonstr = window.localStorage.getItem('jsonstr');
      this.hightLightText();
      this.makeFolding();
    }
    window.onbeforeunload = () => {
      window.localStorage.setItem('jsonstr', this.controller.jsonstr);
    }
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
