<script lang="ts">
  import { page } from '$app/state';
  import Searchbar from '$lib/components/searchbar.svelte';
  import { onMount } from 'svelte';
  let mode: 'search' | 'copy' | 'working' = $state('search');
  let displayText: string = $state('Type a question, click search');
  let value: string = $state('');

  const query: string | null = page.url.searchParams.get('q');

  onMount(() => {
    if (query) value = query;
    mode = 'working';
  });
</script>

<div class="flex flex-col items-center justify-center">
  <img src="images/DuckDuckGo_Logo-Dax_Solo.svg" alt="DuckDuckGo Logo" width="120" />
  <h1 class="w-full pt-3 text-center text-4xl">Let Me DDG That For You...</h1>
</div>

<Searchbar bind:mode bind:displayText bind:value />

<p class="mb-[228px] font-bold">{displayText}</p>
