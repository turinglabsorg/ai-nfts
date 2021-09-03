<template>
  <div id="app">
    <router-view />
  </div>
</template>


<style>
body,
html {
  background: #fff952;
  min-height: 100vh;
}
.home-text {
  padding-left: 60px;
  width:50%;
  float:left;
  text-align:center;
}
.home-images{
  width:50%;
  float:left;
  overflow:hidden;
  height: 100vh;
}
.button {
  font-family: "Major Mono Display", monospace;
  font-size: 30px !important;
  margin-top: 40px;
}
#app {
  font-family: "Major Mono Display", monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #000000;
  margin-top: 0px;
  font-size: 28px !important;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
