<script>
    import { navigate } from "svelte-routing";
    let reviews = [];
    let newReview = "";
    let nome = "";

    function addReview() {
        if (newReview.trim() !== "" && nome != "") {
            reviews = [...reviews, { id: reviews.length, text: nome + ' dice: "' + newReview.trim() + '"' }];
            newReview = "";
            nome = "";
        }
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
    {/each}

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