<script lang="ts">
  import { Copy, Search, X as X_Icon } from 'lucide-svelte';
  import { page } from '$app/state';
  import { blur } from 'svelte/transition';

  type Props = {
    search: boolean;
    displayText: string;
  };

  let { search = $bindable(true), displayText = $bindable('Type a question, click search') }: Props = $props();
  let searchUrl: string = $state(`${page.url.origin}?q=`);
  let value: string = $state('');

  function enterCopyMode() {
    searchUrl += encodeURI(value);
    displayText = 'All done! Share the link above.';
    search = !search;
  }

  async function copyUrl() {
    try {
      await navigator.clipboard.writeText(searchUrl);
      alert('URL copied to clipboard!'); // Optional: Provide user feedback
    } catch (err) {
      console.error('Failed to copy: ', err);
      alert('Failed to copy URL to clipboard.'); // Optional: Inform user of failure
    }
  }
</script>

<div
  class="bg-searchbar shadow-[0 1px 3px rgba(0,0,0,.5)] my-6 flex h-[42px] w-11/12 max-w-[620px]
  items-center justify-center rounded-lg"
>
  {#if search}
    <input in:blur={{ duration: 250 }} bind:value class="caret-ddg-blue50 h-[42px] flex-grow pl-3 outline-none" />
    {#if value.length > 0}
      <button class="hover:text-text h-[42px] cursor-pointer p-2 text-[#999999]" onclick={() => (value = '')}
        ><X_Icon size={18} /></button
      >
    {/if}
    <button
      class="bg-ddg-blue30 hover:bg-ddg-blue40 text-text-dark h-[42px] cursor-pointer rounded-r-lg px-4 py-1.5"
      onclick={enterCopyMode}><Search size={18} /></button
    >
  {:else}
    <div in:blur={{ duration: 250 }} class="flex h-[42px] flex-grow items-center pl-3">{searchUrl}</div>
    <button
      class="hover:text-text h-[42px] cursor-pointer p-2 text-[#999999]"
      onclick={() => {
        value = '';
        search = true;
      }}><X_Icon size={18} /></button
    >
    <button
      class="bg-ddg-blue30 hover:bg-ddg-blue40 text-text-dark h-[42px] cursor-pointer rounded-r-lg px-4 py-1.5"
      onclick={copyUrl}><Copy size={18} /></button
    >
  {/if}
</div>
