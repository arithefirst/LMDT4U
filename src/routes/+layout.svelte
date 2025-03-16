<script lang="ts">
  import Footer from '$lib/components/footer.svelte';
  import Meta from '$lib/components/meta.svelte';
  import type { Snippet } from 'svelte';
  import { Toaster } from 'svelte-sonner';

  // Load Tailwind
  import '$lib/app.css';

  const { children }: { children: Snippet } = $props();
</script>

<Meta />
<main class="bg-base text-text flex h-screen w-screen flex-col items-center justify-center">
  {@render children()}
  <Footer />
</main>
<Toaster
  position="bottom-center"
  toastOptions={{
    unstyled: true,
    classes: {
      toast: 'bg-text-dark text-text border-searchbar w-full rounded-sm border-2 px-3 py-2 text-center',
    },
  }}
/>
