<template>
    <div>
        <div class="text-danger" v-if="jsonstr && jsonerror">{{ jsonerror }}</div>
        <div class="text-success" v-if="!jsonerror">Valid JSON</div>
        <div class="edit_window">
            <textarea class="editor form-control" type="text" 
                @keydown.tab.prevent="{addTab}"
                tabindex="-1"
                v-model="jsonstr" 
                ref="jsonText" 
                placeholder="скопируйте или начните вводить ваш JSON код...">
            </textarea>
            
        </div>
        {{ prettyFormat }}
    </div>
</template>

<script>
export default {
    props: ['buttons'],
    data() {
        return {
            jsonerror: "",
            jsonstr: "",
            lastPosition: 0
        }
    },   
    computed: {
        prettyFormat: function() {
            // reset error
            this.jsonerror = ""
            let jsonValue = ""
            try {
                // try to parse
                jsonValue = JSON.parse(this.jsonstr)
            }
            catch(e) {
                this.jsonerror = JSON.stringify(e.message)
                return ""
            }
            var chekmass = this.jsonstr.split("");
            var lastChar = chekmass[chekmass.length - 1];
            if(this.buttons.autoformation)
                if(lastChar == '}' || lastChar == '\"' || lastChar == ']' || lastChar == ',')
                    setTimeout(() => {
                        this.jsonstr = JSON.stringify(jsonValue, null, 2);
                    }, 100);
        },
        addTab: function() {
            var textarea = this.$refs.jsonText;
            this.lastPosition = textarea.selectionStart;
            this.jsonstr = this.jsonstr.substr(0,this.lastPosition) + "\t" + this.jsonstr.substr(this.lastPosition);
            setTimeout(() => {
                textarea.selectionStart = textarea.selectionEnd =  this.lastPosition + 1;
            }, 1);
        }
    }
}
</script>

<style>
    .edit_window{
        display: flex;
        padding: 5px;
    }
    .editor{
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