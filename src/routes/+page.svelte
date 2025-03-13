<script lang="ts">
  import { Search } from 'lucide-svelte';
</script>

<div class="bg-searchbar flex h-[42px] w-11/12 max-w-[620px] items-center justify-center rounded-lg">
  <input class="caret-ddg-blue50 h-[42px] flex-grow pl-3 outline-none" />
  <button
    class="bg-ddg-blue30 hover:bg-ddg-blue40 text-text-dark h-[42px] cursor-pointer rounded-r-lg px-4 py-1.5"
    onclick={() => console.log('search')}><Search size={18} /></button
  >
</div>
