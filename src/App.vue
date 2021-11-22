<template>
  <div id="app">
    <VirtalScrollWrapper />
  </div>
</template>

<script>

import VirtalScrollWrapper from '@/components/virtual-scroll';
export default {
  name: 'App',
  components: {
    VirtalScrollWrapper
  }
};
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
