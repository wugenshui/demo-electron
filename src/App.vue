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
const exec = require('child_process').exec
const { ipcRenderer } = require('electron')

export default {
  data() {
    return {
      name: 'age'
    }
  },
  mounted() {
    console.log(process.env)
    // 任何你期望执行的cmd命令，ls都可以
    let workerProcess = exec('ipconfig')
    // 打印正常的后台可执行程序输出
    workerProcess.stdout.on('data', function(data) {
      console.log('stdout: ' + data)
    })
    // 打印错误的后台可执行程序输出
    workerProcess.stderr.on('data', function(data) {
      console.log('stderr: ' + data)
    })
    // 退出之后的输出
    workerProcess.on('close', function(code) {
      console.log('out code：' + code)
    })
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
