<template>
  <main>
    <h1>Tic-Tac-Toe</h1>
    <game />
    <footer>Source code available on <a href="https://github.com/brian-petersen/cs260-project03">GitHub</a></footer>
  </main>
</template>

<script>
import Game from './Game';

export default {
  components: {
    'game': Game
  }
};
</script>

<style>
html, body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

body {
  padding-top: 50px;
  background-color: #b5bcc4;
}
</style>

<style scoped>
h1 {
  margin: 0;
  margin-bottom: 50px;
  text-align: center;
  font-size: 60px;
  color: #fff;
  text-shadow: 1px 1px 1px #000;
}

footer {
  text-align: center;
  margin: 30px 0;
  color: #ffffff;
  font-size: 20px;
}

footer a {
  color: #000;
  text-decoration: none;
}

footer a:hover {
  opacity: .8;
}
</style>
