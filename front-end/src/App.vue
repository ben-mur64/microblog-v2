<template>
  <div id="app">
    <div class="site-title"><h1>Microblog</h1></div>
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

.site-title {
  color: #63345e;
  display: flex;
  justify-content: center;
  text-align: center;
  padding: 20px;
}

.site-title h1 {
  font-size: 4rem;
}
</style>
