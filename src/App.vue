<template>
  <div class="app">
      <div class="nav">
          <router-link to="/"><b>AD ASTRA |</b></router-link>
          <router-link to="/about"><b> ABOUT</b></router-link>
          <span>2019 &copy; Mike Stasiak & MvdB Software Solutions</span>
      </div>
    <router-view />
  </div>
</template>

<style lang="scss">

@import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,600,800&display=swap');

* {
  box-sizing: border-box;
}
body {
  font-family: 'Monserrat', sans-serif;
  margin: 0;
  padding: 0;
}

.nav {
  background-color: black;
  height: 7%;
}

a:link {
  color: white;
  text-decoration: none;
}

a:visited {
    color: white;
    text-decoration: none;
}

span {
  text-align: center;
  position: fixed;
  right: 10px;
  color: white;

  @media (max-width: 768px) {
    display: none;
  }
}

</style>
