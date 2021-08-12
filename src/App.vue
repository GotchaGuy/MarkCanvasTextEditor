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
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@600&display=swap');
body {
  background-color: #f1f1f0;
}

</style>
