<template>
  <div id="app">
    <h1>To Do List</h1>
    <HelloWorld/>
    <!-- <p>Ako submitujemo bez clicka na  <em><u>prvi checkbox (ako uopste ne kliknemo) i u input box nista ne ukucamo</u></em>, nastane problem.</p>
    <p>Kad nakon jednog submit-a kliknemo prvi input i submitujemo, prikaze se kako treba u listi ali se prvi checkbox ne vraca na unchecked sam to pokusao.</p> -->
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
body{
  margin:0px;
  padding:0px;
  box-sizing: border-box;
}
</style>
