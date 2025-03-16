<script lang="ts">
  import { Copy, Search, X as X_Icon } from 'lucide-svelte';
  import { page } from '$app/state';
  import { blur } from 'svelte/transition';
  import { toast } from 'svelte-sonner';

  type Props = {
    mode: 'search' | 'copy' | 'working';
    displayText: string;
    value: string;
    workingValue: string;
  };

  let {
    mode = $bindable('search'),
    displayText = $bindable('Type a question, click search'),
    value = $bindable(''),
    workingValue = $bindable(''),
  }: Props = $props();
  let searchUrl: string = $state(`${page.url.origin}?q=`);

  function enterCopyMode() {
    searchUrl += encodeURI(value);
    displayText = 'All done! Share the link above.';
    mode = 'copy';
  }

  async function copyUrl() {
    try {
      await navigator.clipboard.writeText(searchUrl);
      toast('URL copied to clipboard');
    } catch (err) {
      console.error('Failed to copy: ', err);
      toast('Failed to copy URL to clipboard.');
    }
  }
</script>

<div
  class="bg-searchbar shadow-[0 1px 3px rgba(0,0,0,.5)] my-6 flex h-[42px] w-11/12 max-w-[620px]
  items-center justify-center rounded-lg"
>
  {#if mode === 'search'}
    <input
      in:blur={{ duration: 250 }}
      bind:value
      class="caret-ddg-blue50 h-[42px] flex-grow pl-3 outline-none"
      onkeydown={(e) => e.key === 'Enter' && enterCopyMode()}
      placeholder="Search DuckDuckGo..."
    />
    {#if value.length > 0}
      <button class="hover:text-text h-[42px] cursor-pointer p-2 text-[#999999]" onclick={() => (value = '')}
        ><X_Icon size={18} /></button
      >
    {/if}
    <button
      class="bg-ddg-blue30 hover:bg-ddg-blue40 text-text-dark h-[42px] cursor-pointer rounded-r-lg px-4 py-1.5"
      onclick={enterCopyMode}><Search size={18} /></button
    >
  {:else if mode === 'copy'}
    <div in:blur={{ duration: 250 }} class="flex h-[42px] flex-grow items-center pl-3">{searchUrl}</div>
    <button
      class="hover:text-text h-[42px] cursor-pointer p-2 text-[#999999]"
      onclick={() => {
        value = '';
        mode = 'search';
      }}><X_Icon size={18} /></button
    >
    <button
      class="bg-ddg-blue30 hover:bg-ddg-blue40 text-text-dark h-[42px] cursor-pointer rounded-r-lg px-4 py-1.5"
      onclick={copyUrl}><Copy size={18} /></button
    >
  {:else}
    <input
      in:blur={{ duration: 250 }}
      class="caret-ddg-blue50 h-[42px] flex-grow cursor-not-allowed pl-3 outline-none"
      disabled
      aria-disabled={true}
      bind:value={workingValue}
    />
    {#if value.length > 0}
      <button class="h-[42px] cursor-not-allowed p-2 text-[#999999]" disabled aria-disabled={true}
        ><X_Icon size={18} /></button
      >
    {/if}
    <button
      disabled
      aria-disabled={true}
      class="bg-ddg-blue30 text-text-dark h-[42px] cursor-not-allowed rounded-r-lg px-4 py-1.5"
      ><Search size={18} /></button
    >
  {/if}
</div>
