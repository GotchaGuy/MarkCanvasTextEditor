<template>
<!--  <img alt="Vue logo" src="./assets/logo.png">-->
<!--  <HelloWorld msg="Welcome to Your Vue.js App"/>-->
  <text-editor/>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import TextEditor from "./components/TextEditor";


export default {
  name: 'App',
  components: {
    TextEditor
  }
}
</script>
<!--<script src="./lib/fabric.min.js"></script>-->

<style>
#app {
  /*font-family: Avenir, Helvetica, Arial, sans-serif;*/
  /*-webkit-font-smoothing: antialiased;*/
  /*-moz-osx-font-smoothing: grayscale;*/
  /*text-align: center;*/
  /*color: #2c3e50;*/
  /*margin-top: 60px;*/
}
</style>
