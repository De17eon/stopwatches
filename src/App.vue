<template>
  <div id="app">
    <container />
  </div>
</template>

<script>

import container from './components/container'

export default {
  name: 'App',
  components: {
    container
  }
}
</script>

<style>
@font-face {
  font-family: Gotham Pro; 
  src: url(./assets/fonts/GothamPro.ttf); 
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
button:active, button:focus {
  outline: none !important;
}
button::-moz-focus-inner {
  border: 0 !important;
}
button:hover {
  cursor: pointer;
}
body {
  background-color: #353638;
}
path { 
  fill:inherit; 
  stroke:inherit; 
}
</style>
