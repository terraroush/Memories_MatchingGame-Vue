<template>
  <div id="app">
    <matching-game />
  </div>
</template>

<script>
import MatchingGame from "./components/MatchingGame";

export default {
  name: "App",
  components: { MatchingGame },
};
</script>

<style>
body {
  background-color: #121921;
}
h2 {
  margin-top: 8px;
  font-family: 'Caveat', cursive;
  letter-spacing: 2px;
font-size: 30px;
}
h1 {
  font-family: 'Poiret One', cursive;
  font-size: 45px;
}
#app {
  font-family: Avenir, Helvetica, Arial;
  text-align: center;
}
</style>
