<template>
    <div>
        <div>
            <div class="text-danger" v-if="controller.jsonstr && jsonerror">{{ jsonerror }}</div>
            <div class="text-success" v-if="!jsonerror">Valid JSON</div>
            <div class="edit_window">
                <textarea class="editor form-control" type="text" 
                    @keydown.tab.prevent="{addTab}"
                    tabindex="-1"
                    @input="{prettyFormat,makeLog,hightLightText}"
                    v-model="controller.jsonstr" 
                    ref="jsonText" 
                    placeholder="скопируйте или начните вводить ваш JSON код...">
                </textarea>
                <div contenteditable="true" class="hightlighter_box" ref="jsonBack">
                    <pre class="hightlighter" v-html="controller.jsonhtml"></pre>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['controller'],
    data() {
        return {
            jsonerror: ""
        }
    },   
    computed: {
        prettyFormat: function() {
            this.jsonerror = ""
            let jsonValue = ""

            try {
                jsonValue = JSON.parse(this.controller.jsonstr)

                var chekmass = this.controller.jsonstr.split("");
                var lastChar = chekmass[chekmass.length - 1];

                if(this.controller.autoformation)
                    if(lastChar == '}' || lastChar == '\"' || lastChar == ']' || lastChar == ',')
                        setTimeout(() => {
                            this.controller.jsonstr = JSON.stringify(jsonValue, null, 2);
                            this.hightLightText();
                        }, 100);
            }
            catch(e) {
                this.jsonerror = JSON.stringify(e.message)
                return ""
            }
        },
        addTab: function() {
            var textarea = this.$refs.jsonText;
            var textback = this.$refs.jsonBack
            var lastPosition = textarea.selectionStart;
            this.controller.jsonstr = this.controller.jsonstr.substr(0,lastPosition) + "\t" + this.controller.jsonstr.substr(lastPosition);
            setTimeout(() => {
                textarea.selectionStart = textarea.selectionEnd =  lastPosition + 1;
            }, 1);
        },
        makeLog: function() {
            if(this.controller.iterator >= this.controller.stringlog.length){
                this.controller.stringlog.splice(-(this.controller.stringlog.length - this.controller.iterator));
                this.controller.iterator = this.controller.stringlog.length - 1; 
            }
            this.controller.stringlog.push(this.controller.jsonstr);
            this.controller.iterator += 1;
        },
        hightLightText: function(){
            this.controller.jsonhtml = this.controller.jsonstr.replace(/"(\w*|\s*|\d*)*"/gi, str => "<span style=\"color: red;\">" + str + "</span>");
        }
    }
}
</script>

<style>
    .hightlighter_box{
        z-index: -1;
        position: absolute;
        width: 90%;
        top: 8px;
        left: 6px;
        letter-spacing: 0.18px;
    }
    .hightlighter{
        text-align: start;
        padding-left: 15px;
        margin: 0;
    }
    .edit_window{
        position: relative;
        display: flex;
        padding: 5px;
    }
    .editor{    
        background: none;
        color: rgba(0, 0, 0, 0.5);
        padding-left: 15px;
        width: 100%;
        height: 300px;
        resize: none;
    }
    .text-success{
        color: green;
    }
    .text-danger{
        color: red;
    }
</style>