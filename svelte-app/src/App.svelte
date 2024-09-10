<script>
  import Router from "svelte-spa-router";
  import routes from "./routes";
</script>

<main>
  <Router {routes} />
</main>

<style>
  main {
    text-align: center;
    padding: 0px;
    overflow: hidden;
    margin: 0px;
	height: 100vh;
    width: 100vw;
  }
</style>
