<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

input, select {
  margin: 5px;
  border: solid 1px rgba(0,0,0,0.21);
  border-radius: 3px;
  padding: 5px;
}

input:focus, select:focus {
  border: solid 1px rgba(0,0,0,0.21);
  outline: none;
}

button {
  padding: 8px;
  margin: 2px;
  box-shadow: unset;
  border: solid 1px white;
  border-radius: 5px;
  cursor: pointer;
}

label {
  margin-left: 5px;
  font-size: 12px;
}
</style>
