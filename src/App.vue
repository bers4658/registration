<template>
<div>
  <Registration></Registration>
</div>
</template>

<script>

import Registration from '../src/components/Registration.vue'
export default {
  name: 'App',
  components: {
    Registration
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
</style>
