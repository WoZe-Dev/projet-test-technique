<template>
  <div id="app">
    <HelloWorld />
    <Homepage />
     <!-- Ajoutez cette ligne -->
    <!-- Reste de votre contenu -->
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import Homepage from './components/Homepage.vue';


export default {
  name: 'App',
  components: {
    HelloWorld,
    Homepage,
    
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  
}

body {
  background-color: #302E44;  /* Changez cette valeur pour la couleur de votre choix */
}

@media (max-width: 576px) {
  #app{
    margin-top: 0px;
    
  }
}


</style>
