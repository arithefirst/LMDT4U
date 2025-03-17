<script lang="ts">
  import { page } from '$app/state';

  let query: string | null = page.url.searchParams.get('q');
  if (query) query = decodeURI(query);
</script>

<svelte:head>
  <!-- HTML Meta Tags -->
  <title>Let Me DDG That</title>
  <meta
    name="description"
    content={query
      ? `For all those people that find it more convenient to bother you than to search "${query}" on DuckDuckGo for themselves.`
      : 'For all those people that find it more convenient to bother you with their question than to search it on DuckDuckGo for themselves.'}
  />

  <!-- Google / Search Engine Tags -->
  <meta itemprop="name" content={query ? `"${query}"` : 'Let Me DDG That'} />
  <meta
    itemprop="description"
    content={query
      ? `For all those people that find it more convenient to bother you than to search "${query}" on DuckDuckGo for themselves.`
      : 'For all those people that find it more convenient to bother you with their question than to search it on DuckDuckGo for themselves.'}
  />
  <meta itemprop="image" content="https://lmdt4u.vercel.app/favicon.png" />

  <!-- Facebook Meta Tags -->
  <meta property="og:url" content="https://lmdg4u.vercel.app" />
  <meta property="og:type" content="website" />
  <meta property="og:title" content={query ? `"${query}"` : 'Let Me DDG That'} />
  <meta
    property="og:description"
    content={query
      ? `For all those people that find it more convenient to bother you than to search "${query}" on DuckDuckGo for themselves.`
      : 'For all those people that find it more convenient to bother you with their question than to search it on DuckDuckGo for themselves.'}
  />
  <meta property="og:image" content="https://lmdt4u.vercel.app/favicon.png" />

  <!-- Twitter Meta Tags -->
  <meta name="twitter:card" content="summary_large_image" />
  <meta name="twitter:title" content={query ? `"${query}"` : 'Let Me DDG That'} />
  <meta
    name="twitter:description"
    content={query
      ? `For all those people that find it more convenient to bother you than to search "${query}" on DuckDuckGo for themselves.`
      : 'For all those people that find it more convenient to bother you with their question than to search it on DuckDuckGo for themselves.'}
  />
  <meta name="twitter:image" content="https://lmdt4u.vercel.app/favicon.png" />
</svelte:head>
