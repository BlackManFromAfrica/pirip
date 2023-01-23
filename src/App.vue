<template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav>
  <router-view />
</template>
<script>
</script>
<style>
@tailwind base;
@tailwind components;
@tailwind utilities;
html{
  background-color: rgb(218, 218, 218);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>





 <!-- <input type="text" style="border: 1px solid black" />
    <button onclick="parse()">Получить информацию</button>
    <p id="wiki"></p>
  <script>
    const parse = async () => {
      const url =
        `https://ru.wikipedia.org/w/api.php?` +
        new URLSearchParams({
          origin: "*",
          action: "parse",
          page: `${document.querySelector("input").value}`,
          format: "json",
        });

      try {
        const req = await fetch(url);
        const json = await req.json();
        console.log(json.parse.text["*"]);
        const wikiContainer = document.querySelector("#wiki");
        wikiContainer.innerHTML = json.parse.text["*"];
        wikiContainer.innerHTML = document.querySelector('b').parentNode.outerHTML
      } catch (e) {
        console.error(e);
      }
    };
  </script> -->
