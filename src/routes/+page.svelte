<script lang="ts">
  import { page } from '$app/state';
  import Pointer from '$lib/components/pointer.svelte';
  import Searchbar from '$lib/components/searchbar.svelte';
  import { onMount } from 'svelte';
  import { blur } from 'svelte/transition';

  // Searchbar data
  let mode: 'search' | 'copy' | 'working' = $state('search');
  let displayText: string = $state('');
  let value: string = $state('');
  let workingValue: string = $state('');

  // Pointer data
  let x = $state(16);
  let y = $state(16);

  const query: string | null = page.url.searchParams.get('q');

  function sleep(n: number): Promise<void> {
    return new Promise((resolve) => setTimeout(resolve, n));
  }

  onMount(async () => {
    if (query) {
      mode = 'working';
      displayText = 'Step 1. Type your question';
      await sleep(1500);
      for (const c of decodeURI(query)) {
        workingValue += c;
        await sleep(69);
      }
    } else {
      displayText = 'Type a question, click search';
    }
  });
</script>

{#if mode == 'working'}
  <Pointer bind:x bind:y />
{/if}

<div class="flex flex-col items-center justify-center">
  <img src="images/DuckDuckGo_Logo-Dax_Solo.svg" alt="DuckDuckGo Logo" width="120" />
  <h1 class="w-full pt-3 text-center text-4xl">Let Me DDG That For You...</h1>
</div>

<Searchbar bind:mode bind:displayText bind:value bind:workingValue />

{#key displayText}
  <p in:blur class="mb-[228px] h-6 font-bold">{displayText}</p>
{/key}
