<script>
  import { goto } from '$app/navigation';

  const startTest = () => {
    goto('/test');
  }
</script>

<button on:click={startTest}>Start Test</button>
