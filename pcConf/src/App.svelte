<script>
    import { Router, Route } from "svelte-routing";
    import main from "./main.svelte";
    import reviews from "./reviews.svelte";
    import intel from "./intel.svelte";
    import amd from "./amd.svelte";
    import cart from "./cart.svelte";
  </script>
  
  <Router>
    <Route path="/" component={main} />
    <Route path="/reviews" component={reviews} />
    <Route path="/intel" component={intel} />
    <Route path="/amd" component={amd} />
    <Route path="/cart" component={cart} />
    
  </Router>
  
  <style>
    
  </style>