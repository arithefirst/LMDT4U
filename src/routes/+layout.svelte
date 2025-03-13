<script lang="ts">
  import type { Snippet } from 'svelte';
  const { children }: { children: Snippet } = $props();

  // Load Tailwind
  import '$lib/app.css';
</script>

<main class="bg-base text-text flex h-screen w-screen flex-col items-center justify-center">
  {@render children()}
  <footer class="absolute bottom-2 w-full text-center text-xs">
    The DuckDuckGo name, logos, trade dress, and other brand elements are trademarks of Duck Duck Go, Inc. For more information, see
    <a href="/ddg-brand-guidelines.pdf" target="_blank" class="text-sky-500 underline hover:text-sky-600">ddg-brand-guidelines.pdf</a>
  </footer>
</main>
