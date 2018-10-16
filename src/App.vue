<template>
  <div id="app">
    <h1>好好学日语，天天背单词</h1>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
  html, body {
    height: 100%;
    width: 100%;
    margin: 0;
    overflow-y: hidden;
  }

  #app {
    height: 100%;
    width: 100%;
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    overflow-y: hidden;
    display: flex;
    flex-direction: column;
  }
</style>
