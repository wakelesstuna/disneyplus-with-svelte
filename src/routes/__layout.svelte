<script>
  import NavBar from "../components/NavBar.svelte";
  import "../styles/global.css";
</script>

<header>
  <NavBar />
</header>
<main>
  <slot />
</main>
<footer>
  <p>Copyright 2022 wakelesstuna</p>
</footer>

<style>
  header {
    position: fixed;
    left: 0;
    top: 0;
    min-height: 75px;
    width: 100vw;
    z-index: 10;
  }
  main {
    max-width: 100%;
    margin: 20px auto;
    min-height: 100vh;
    margin-top: 100px;
  }
  footer {
    background-color: #181b24;
    min-height: 200px;
    display: flex;
    align-items: center;
    justify-content: center;
  }
</style>
