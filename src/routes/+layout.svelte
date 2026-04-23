<script>
    import '../app.css';
    import Header from '$lib/components/Header.svelte';
    import Footer from '$lib/components/Footer.svelte';
</script>

<div class="app">
    <Header />

    <main>
        <slot />
    </main>

    <Footer />
</div>

<style>
    .app {
        display: flex;
        flex-direction: column;
        min-height: 100vh;
        width: 100%;
        max-width: 1280px;
        margin: 0 auto;
        padding: 0 var(--spacing-md);
    }

    main {
        flex: 1;
        padding-top: var(--spacing-xl);
    }
</style>
