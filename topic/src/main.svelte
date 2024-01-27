<script>
  import { navigate } from "svelte-routing";
  
  function goToReviewsPage() {
    navigate("/reviews");
  }

  function goToIntelPage() {
    navigate("/intel");
  }

  function goToAmdPage() {
    navigate("/amd");
  }
</script>

<main>
  <h1>Homepage</h1>
  <button on:click={goToReviewsPage}>Vai alle Recensioni</button>
  <button on:click={goToIntelPage}>Configurazione Intel</button>
  <button on:click={goToAmdPage}>Configurazione AMD</button>
</main>

<style>
  main {
    text-align: center;
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
  }
</style>