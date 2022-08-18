<template>
<nav class="navbar navbar-light bg-light">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">
      
      <h2>Acidosis Metabólica</h2>
    </a>
  </div>
</nav>
<br/>
<br/>
<br/>

<div class="container">
<HelloWorld/>
</div>
  
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import bootstrap from  'bootstrap'
export default {
  name: 'App',
  components: {
    HelloWorld
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
@import'~bootstrap/dist/css/bootstrap.css'
</style>
