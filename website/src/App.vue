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
  width: 50%;
  float: left;
  text-align: center;
}
.home-images {
  width: 50%;
  float: left;
  overflow: hidden;
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
.title-drop{
  font-size:60px!important;
}
@media screen and (max-width: 768px) {
  .home-images {
    width: 100%;
    position: fixed;
    z-index: 5;
  }
  .home-text {
    width: 100%;
    position: absolute;
    z-index: 10;
    padding: 10px;
    background-color: rgba(255, 249, 82, 0.8);
    min-height: 100vh;
    padding-bottom:80px;
  }
  #app {
    font-size: 25px !important;
  }
  .button {
    font-size: 20px !important;
    margin-top: 40px;
  }
.title-drop{
  font-size:30px!important;
}
}
</style>
