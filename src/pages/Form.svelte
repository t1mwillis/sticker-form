<script>
  import { navigate,Link } from "svelte-routing";

  let name = ''
	let email = ''
	let address = ''
	let message = ''
	let subscribe = true

	let hasSubmitted = false

	$: valid = {
		name: name.length > 4,
		email: email.includes('@') && email.includes('.'),
		address: address.length > 10
	}

	const validateAndSend = (e) => {
		e.preventDefault()
		hasSubmitted = true
		if (valid.name && valid.email && valid.address) {
			console.log('I can submit the form!')

			console.log(JSON.stringify({
				name,
				email,
				subscribe: subscribe ? 'true' : 'false',
				address,
				message
			})
      )
      navigate("/thank-you", { replace: true });
		}
	}
</script>
<section>
	<!-- {@debug STATE} -->
  <Link to="/thank-you">Thanks</Link>
	<h1 class="cont-title">Get some Stickers!</h1>
	<div class="contact-info">
    <form role="form" name="feedbackForm" class="contactForm" on:input="{hasSubmitted = false}" on:submit={validateAndSend} >
      <div class="form-group">
        <div class="label-wrap">
          <label for="name">Name</label>
        </div>
        <input type="text" name="contactName" class="form-control" id="name" placeholder="Your Name" min="4" bind:value="{name}">
        {#if !valid.name && hasSubmitted}
          <div class="validation" style="display: block;">Please enter at least 4 chars</div>
        {/if}
      </div>
      <div class="form-group">
        <div class="label-wrap">
          <label for="email">Email</label>
        </div>
        <input type="email" class="form-control" name="email" id="email" placeholder="email@domain.com" bind:value="{email}">
        {#if !valid.email && hasSubmitted}
          <div class="validation" style="display: block;">Please enter a valid email</div>
        {/if}
        <div class="label-wrap">
          <input type="checkbox" class="form-control" name="subscribe" id="subscribe" bind:checked="{subscribe}">
          <label for="subscribe">Subscribe to my extremely infrequent newsletter</label>
        </div>
      </div>
      <div class="form-group">
        <div class="label-wrap">
          <label>Address</label>
          <span>&nbsp;- Anywhere in the world, just make sure it's correct!</span>
        </div>
        <textarea class="form-control" name="address" rows="5" placeholder="Your Address" bind:value="{address}"></textarea>
        {#if !valid.address && hasSubmitted}
          <div class="validation" style="display: block;">Please provide your address</div>
        {/if}
      </div>
      <div class="form-group">
        <div class="label-wrap">
          <label>Message</label>
          <span>&nbsp;- Only want one kind of sticker? Think this is cool?</span>
        </div>
        <textarea class="form-control" name="message" rows="5" data-rule="required" data-msg="Please write something for us" placeholder="Your Message" bind:value="{message}"></textarea>
      </div>
      <button type="submit" class="btn btn-send">Send</button>
    </form>
  </div>
</section>

<style>
  input[type="text"], input[type="email"], textarea, button {
    width: 100%;
  }

  .label-wrap label {
    font-weight: bold;
  }

  .label-wrap span {
    font-style: italic;
  }

  .label-wrap {
    display: flex;
    margin-bottom: .5em;
  }

  label[for="subscribe"] {
    flex-grow: 1;
    font-weight: normal;
    margin-left: .5em;
  }

  .form-group {
    margin-bottom: 1em;
  }

  .validation {
    color: #ff3e00;
  }

  section {
    max-width: 600px;
    margin: 0 auto;
    padding: 0 1em;
  }
</style>
