<script>
  import { writable } from 'svelte/store';
  import { goto } from '$app/navigation';

  let email = writable("");

  const submitEmail = () => {
    goto('/review_result');
  }
</script>

<input type="email" bind:value={$email} placeholder="Enter your email (optional)" />
<button on:click={submitEmail}>Submit</button>
