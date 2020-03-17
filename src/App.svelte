<script>
  import { Router, Link, Route } from "svelte-routing";
  import Form from "./pages/Form.svelte";
  import ThankYou from "./pages/ThankYou.svelte";

  export let url = "";
</script>

<Router url="{url}">
	<Route path="/thank-you" component="{ThankYou}" />
	<Route path="/" component="{Form}" />
</Router>