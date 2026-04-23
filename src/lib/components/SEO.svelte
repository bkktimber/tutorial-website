<script>
    /** @type {{ title?: string, description?: string, ogImage?: string, canonicalUrl?: string }} */
    let { title = 'Mai', description = '', ogImage = '', canonicalUrl = '' } = $props();

    const fullTitle = $derived(title === 'Mai' ? title : `${title} — Mai`);
</script>

<svelte:head>
    <title>{fullTitle}</title>
    {#if description}
        <meta name="description" content={description} />
    {/if}

    <!-- Open Graph -->
    <meta property="og:title" content={fullTitle} />
    {#if description}
        <meta property="og:description" content={description} />
    {/if}
    {#if ogImage}
        <meta property="og:image" content={ogImage} />
    {/if}
    {#if canonicalUrl}
        <meta property="og:url" content={canonicalUrl} />
    {/if}
    <meta property="og:type" content="website" />

    <!-- Twitter Card -->
    <meta name="twitter:card" content="summary_large_image" />
    <meta name="twitter:title" content={fullTitle} />
    {#if description}
        <meta name="twitter:description" content={description} />
    {/if}
    {#if ogImage}
        <meta name="twitter:image" content={ogImage} />
    {/if}

    <!-- Canonical -->
    {#if canonicalUrl}
        <link rel="canonical" href={canonicalUrl} />
    {/if}
</svelte:head>
