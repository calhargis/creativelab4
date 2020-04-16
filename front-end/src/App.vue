<template>
<div id="app">
  <div class="header">
    <router-link to="/">

    </router-link>
    <div class="navbar">
    <br>
      <router-link to="/admin">Admin |</router-link>
      <router-link to="/"> Home |</router-link>
      <router-link to="/about"> About</router-link>
      <p></p>
    </div>
    <div class="title">
    <br><br><br>
      <h1>All About Jacob</h1>
    </div>
  </div>
  <div class="content">
    <router-view />
  </div>
  <div class="footer">
    <a href="https://github.com/calhargis/creativelab4">GitHub</a>
  </div>
</div>
</template>

<style>
html {
  box-sizing: border-box;
}

body {
  font-family: Arial;
  font-size: 16px;
  background: #fff;
  padding: 0px;
  margin: 0px;
}

/* Header */
.header {
  text-align: center;

}

.title {
  margin-top: 5px;
}

.title h1 {
  font-size: 30px;
}

.content {
  padding: 20px 100px;
  min-height: 500px;
}

/* Footer */
.footer {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  text-align: center;
}

.navbar {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  text-align: center;
  background-color: red;
  color: white;
}

h1 {
  font-size: 20px;
}

h2 {
  font-size: 14px;
}
</style>
