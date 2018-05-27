<template>
  <div>
    <!-- <app-header></app-header> -->
    <router-view/>
  </div>
</template>

<script>
import AppHeader from './components/Toolbar'
export default {
  name: 'App',
  replace: false,
  components: {
    AppHeader
  }
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
</style>
