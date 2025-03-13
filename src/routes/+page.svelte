<script lang="ts">
  import { Search } from 'lucide-svelte';
</script>

<div class="bg-searchbar flex h-[42px] w-11/12 max-w-[620px] items-center justify-center rounded-lg px-3">
  <input class="h-[42px] flex-grow" />
  <button class="h-[42px] cursor-pointer p-1.5 text-[#A5A5A5]" onclick={() => console.log('search')}><Search size={18} /></button>
</div>
