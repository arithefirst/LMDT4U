<script lang="ts">
  import type { Snippet } from 'svelte';
  const { children }: { children: Snippet } = $props();

  // Load Tailwind
  import '$lib/app.css' 
</script>

{@render children()}