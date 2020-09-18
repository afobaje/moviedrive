<template>
  <div id="app">
    <header>
      <span id="logo"><h1><a href="http://">moviedrive</a></h1></span>
      
    </header>
    
    <recipe></recipe>
    
    <footer>Made with love by <a href="http://twitter.com/davidblaqq">BLACK BOY</a></footer>
  </div>
</template>

<script>
/*import HelloWorld from './components/HelloWorld.vue'*/
import recipe from './components/recipe.vue'

export default {
  name: 'App',
  components: {
    /*HelloWorld,*/
    recipe
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Bangers&display=swap'),
url('https://fonts.googleapis.com/css2?family=Poppins&display=swap');
$button-color: #0095f6;
*{
  margin: 0;
  padding: 0;
}
header{
  height: 10vh;
  position: sticky; 
  
  display: flex;
  /*text-align: start;*/
  justify-content: center;
  font-family: 'Poppins', sans-serif;
  
}
#logo{
  margin-top: 1em;
  h1{
    a{
      color: black;
      text-decoration: none;
      
    }
  }
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: calc(100vh-70px);
  margin: 0;
  display: flex;
  flex-direction: column;
}
footer{
  flex-shrink: 0;
  height: 50px;
  position: relative;
  margin-top: 50vh;
  font-family: 'Bangers', cursive;
  //font-family: 'Poppins', sans-serif;
  a{
    text-decoration: none;
    color: $button-color;
    font-weight: 600;
    &:hover{
      text-decoration: underline;
    }
  }
}
</style>