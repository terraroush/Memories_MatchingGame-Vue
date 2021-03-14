<template>
  <div id="app">
   <matching-game />
   
  </div>
</template>

<script>
import MatchingGame from './components/MatchingGame';

export default {
  name: "App",
  components: { MatchingGame },
  
};
</script>

<style>
body {
  background-color: #121921;
}
#app {
  font-family: Avenir, Helvetica, Arial;
  text-align: center;
}
</style>
