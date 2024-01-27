<script>
  import { navigate } from "svelte-routing";
  import { onMount } from "svelte";

  let reviews = [];
  let newReview = "";
  let nome = "";

  onMount(() => {
    // Carica le recensioni dal localStorage all'avvio dell'applicazione
    const savedReviews = localStorage.getItem("reviews");
    reviews = savedReviews ? JSON.parse(savedReviews) : [];
  });

  function addReview() {
      if (newReview.trim() !== "" && nome != "") {
          const updatedReviews = [...reviews, { id: reviews.length, text: nome + ' dice: "' + newReview.trim() + '"' }];
          reviews = updatedReviews;
          newReview = "";
          nome = "";
          localStorage.setItem("reviews", JSON.stringify(updatedReviews));
      }
  }

  function deleteReview(id) {
    // Filtra le recensioni rimuovendo quella con l'id specificato
    const updetedReviews = reviews.filter((review) => review.id !== id);
    reviews = updetedReviews;
    // Salva le recensioni aggiornate nel localStorage
    localStorage.setItem("reviews", JSON.stringify(updetedReviews));
  }

function goToHomePage() {
  navigate("/");
}
</script>

<main>
  
  <h1>Recensioni</h1>
  <div>
      <input class="recensione" bind:value={nome} placeholder="Nome">
      <textarea class="recensione" bind:value={newReview} placeholder="Aggiungi una recensione"></textarea>
      <button on:click={addReview}>Aggiungi Recensione</button>
  </div>

  {#each reviews as review (review.id)}
      <p>{review.text}</p>
      <button on:click={() => deleteReview(review.id)}>Elimina</button>
  {/each}<br>

  <button on:click={goToHomePage}>Homepage</button>
      
</main>

<style>
  main {
  text-align: center;
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

.recensione {
  width: 100%;
  margin-bottom: 10px;
}
</style>