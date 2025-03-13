<script lang="ts">
  import Searchbar from '$lib/components/searchbar.svelte';
  let search: boolean = $state(true);
  let displayText: string = $state('Type a question, click search');
</script>

<div class="flex flex-col items-center justify-center">
  <img src="images/DuckDuckGo_Logo-Dax_Solo.svg" alt="DuckDuckGo Logo" width="120" />
  <h1 class="w-full pt-3 text-center text-4xl">LMTD4U</h1>
</div>

<Searchbar bind:search bind:displayText />

<p class="mb-[228px] font-bold">{displayText}</p>
