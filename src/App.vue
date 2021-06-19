<template>
    <dir id="app">
      <UserProfile />
    </dir>
    
</template>

<script>

import UserProfile from "./components/UserProfile.vue";


export default {
    name: 'App',
    components: { UserProfile },
    

}
    

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: rgb(29, 25, 19);
  min-height: 100vh;
  background-color: rgb(197, 216, 210);
}
</style>
