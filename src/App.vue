<template>
  <div id="app">
    <img src="./assets/logo.png" style="margin: 0 auto;">
    
    <filmstrip media-id="32149"/>
    <HelloWorld/>
    <filmstrip media-id="37880"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import filmstrip from './components/filmstrip'


export default {
  name: 'App',
  props: ['mediaId'],
  components: {
    HelloWorld,
    filmstrip
  },
  data(){
    return {
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
  margin: 60px auto 0;
  width: 1000px;
  overflow: hidden;
}
#app img{
  display: block;
}
</style>
