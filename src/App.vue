<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
      <button @click="auto">自定义事件</button>
    </div>
    <router-view />
  </div>
</template>

<script>
const { require } = window
const { ipcRenderer } = require('electron')

export default {
  data() {
    return {
      name: 'age'
    }
  },
  mounted() {
    console.log(process.env)
  },
  methods: {
    auto() {
      ipcRenderer.invoke('perform-action', 1, 2)
    }
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

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
