<template>
  <div class="container">
    <h1 class="heading">Random Quote Generator</h1>
    <RandomQuote />
  </div>
  
</template>

<script>
import RandomQuote from './components/RandomQuote.vue'

export default {
  name: 'App',
  components: {
    RandomQuote
  }
}
</script>

<style>
.container {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 10%;

 
}

.heading{
  font-size: 2rem; 
  font-weight: 500;
margin-bottom: 20px;
color: #fff;

}
*{
  /* background: #CCCCFF; */
  margin: 0;
  padding: 0;
}
body{
  background: #00416A;
}

@media screen and (max-width: 768px){
  .heading{
    font-size: 1.5rem;
  }
  .container{
    margin-top: 20%;
  }
}
</style>
