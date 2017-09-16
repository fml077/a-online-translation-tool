<template>
  <div id="app">
    <h3>在线翻译小工具</h3>
    <h5 class="text-muted">支持多种语言</h5>
    <translateForm v-on:formSubmit="translateText"></translateForm>
    <translateOutput v-text="translatedText"></translateOutput>
  </div>
</template>

<script>

import TranslateForm from './components/TranslateForm'
import TranslateOutput from './components/TranslateOutput'

export default {
  name: 'app',
  data:function(){
    return{
      translatedText:""
    }
  },
  components: {
    TranslateForm,TranslateOutput
  },
  methods:{
    /*
    *@param: text  string  the content to translate
    *@param: language  string  the language to translate to
    */

    translateText:function(text,language){
      // alert(text);
      this.$http.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20170916T094535Z.18d1fe99ff146c88.0fa25a42bad7a1c2f5dff7df8bd65d9ff18780b6&lang='+language+'&text='+text)
          .then((response)=>{
            // console.log(response.body.text[0]);
            this.translatedText = response.body.text[0];
          })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
