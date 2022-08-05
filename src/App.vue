<template>
  <div id="app">
    <Pomodoro />
  </div>
</template>

<script>

import Pomodoro from './components/Pomodoro'

export default {
  name: 'App',
  components: {
    Pomodoro
  }
}
</script>

<style>
#app {
  margin: auto;
  width: 90%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
