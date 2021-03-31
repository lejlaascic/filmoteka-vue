<template>
  <header>
    <router-link to="/">
      <h1><span>Vue</span>Movies</h1>
    </router-link>
  </header>
  <main>
    <router-view></router-view>
  </main>
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Source Sans Pro", sans-serif;
  &::selection {
    background: transparentize(#77aaff, 0.5);
  }
}
body {
  background-color: #35495e;
}
a {
  text-decoration: none;
}
header {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 16px;
  background-color: #2c3d4e;
  box-shadow: 0px 0px 6px rgba(0, 0, 0, 0.1);
  h1 {
    color: #fff;
    font-size: 1.5rem;
    span {
      color: #42bb83;
    }
  }
}
@media screen and (max-width: 690px) {
  header {
    padding: 16px;
    h1 {
      font-size: 1.5rem;
    }
  }
}
@media screen and (min-width: 1025px) {
  header {
    padding: 19px;
    h1 {
      font-size: 1.7rem;
    }
  }
}
@media screen and (min-width: 1600px) {
  header {
    padding: 20px;
    h1 {
      font-size: 2rem;
    }
  }
}
</style>
