<script>
  import { writable } from 'svelte/store';
  import { goto } from '$app/navigation';
  import { questions } from '$lib/database'; // Assuming your questions are in this file

  // Reactive store for the current question index
  let currentQuestionIndex = writable(0);

  // Get the current question based on the index
  $: currentQuestion = questions[$currentQuestionIndex];

  // Handlers for Yes and No buttons
  const handleAnswer = () => {
    if ($currentQuestionIndex < questions.length - 1) {
      currentQuestionIndex.update(n => n + 1);
    } else {
      goto('/submit_email'); // Move to the next screen when the last question is answered
    }
  }
</script>

<!-- Display the current question -->
<textarea readonly bind:value={currentQuestion}></textarea>

<!-- Buttons to answer the question -->
<button on:click={handleAnswer}>Yes</button>
<button on:click={handleAnswer}>No</button>

<style>
  textarea {
    width: 100%;
    height: 100px;
    margin-bottom: 1rem;
  }

  button {
    margin-right: 1rem;
  }
</style>
