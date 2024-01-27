<script>
    import { navigate } from "svelte-routing";

    function goToHomePage(){
        navigate("/");
    }

</script>

<main>
    <h1>Carrello</h1>
    <button on:click={goToHomePage}>Homepage</button>
</main>
