<template>
  <div id="app">
    <nav>ShareScreen.io</nav>
    <router-view />
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {},
  data: () => ({
    box: {
      text: 'Record your screen and share it with someone else, you can do realtime sharing with someone and you will be the one in control of what part of your screen you\'d want to be shared/recorded! When you\'re done you could alslo download the recording for even more use cases.'
    }
  })
}
</script>

<style>
html, body {
  margin: 0;
  padding: 0;
  background: #ccc;
}

nav {
  width: 100%;
  height: 20px;
  background: rgba(0, 0, 0, 0.7);
  padding: 10px;
  color: whitesmoke;
  font-weight: bold;
  font-size: 1em;
}

#app {
  background: white;
  border-bottom: 3px solid #888;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 0px;
  padding: 0 0 10px;
}

.center {
  display: flex;
  padding: 15px;
  text-align: left;
  border-left: 10px solid #4caf50;
  background: #000000ab;
  color: #f5f5f5;
  box-shadow: 0 3px 3px rgba(0,0,0,0.4);
  font-weight: bold;
  font-size: 1.1em;
}

.center .icon {
  font-size: 62px;
  margin-right: 15px;
}

.container {
  margin: 10px;
}
</style>
