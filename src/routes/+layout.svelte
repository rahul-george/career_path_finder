<script>
	import { page } from '$app/stores';
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';
  
	let visitedScreens = {
	  start: false,
	  test: false,
	  submitEmail: false,
	  reviewResult: false
	};
  
	onMount(() => {
	  const currentRoute = $page.url.pathname;
  
	  if (currentRoute === '/start') {
		visitedScreens.start = true;
	  } else if (currentRoute === '/test' && visitedScreens.start) {
		visitedScreens.test = true;
	  } else if (currentRoute === '/submit_email' && visitedScreens.test) {
		visitedScreens.submitEmail = true;
	  } else if (currentRoute === '/review_result' && visitedScreens.submitEmail) {
		visitedScreens.reviewResult = true;
	  } else {
		goto('/start');
	  }
	});
  
	$: {
	  const currentRoute = $page.url.pathname;
  
	  // Ensure the user is redirected if they attempt to bypass steps
	  if (currentRoute === '/test' && !visitedScreens.start) {
		goto('/start');
	  } else if (currentRoute === '/submit_email' && !visitedScreens.test) {
		goto('/test');
	  } else if (currentRoute === '/review_result' && !visitedScreens.submitEmail) {
		goto('/submit_email');
	  }
	}
  </script>
  
  <main>
	<slot />
  </main>
  
  <style>
	main {
	  display: flex;
	  justify-content: center;
	  align-items: center;
	  min-height: 100vh;
	  padding: 1rem;
	  box-sizing: border-box;
	}
  </style>
  