<script>
    import { page } from '$app/state';

    const navLinks = [
        { href: '/', label: 'Home' },
        { href: '/about', label: 'About' }
    ];

    let mobileOpen = $state(false);

    function toggleMobile() {
        mobileOpen = !mobileOpen;
    }

    function closeMobile() {
        mobileOpen = false;
    }
</script>

<header class="sticky top-0 z-50 bg-[var(--color-bg)]/95 backdrop-blur-sm border-b border-[var(--color-border)]">
    <nav class="max-w-5xl mx-auto px-6 py-4 flex items-center justify-between">
        <a href="/" class="font-heading text-2xl text-[var(--color-text)] hover:text-[var(--color-accent)] transition-colors duration-200" onclick={closeMobile}>
            Mai
        </a>

        <!-- Desktop nav -->
        <ul class="hidden md:flex items-center gap-8">
            {#each navLinks as link}
                <li>
                    <a
                        href={link.href}
                        class="text-sm font-medium tracking-wide uppercase transition-colors duration-200
                            {page.url.pathname === link.href
                                ? 'text-[var(--color-accent)]'
                                : 'text-[var(--color-text-secondary)] hover:text-[var(--color-text)]'}"
                    >
                        {link.label}
                    </a>
                </li>
            {/each}
        </ul>

        <!-- Mobile hamburger -->
        <button
            class="md:hidden flex flex-col gap-1.5 p-2 -mr-2"
            onclick={toggleMobile}
            aria-label="Toggle navigation"
            aria-expanded={mobileOpen}
        >
            <span class="block w-5 h-0.5 bg-[var(--color-text)] transition-all duration-200 origin-center {mobileOpen ? 'rotate-45 translate-y-[4px]' : ''}"></span>
            <span class="block w-5 h-0.5 bg-[var(--color-text)] transition-all duration-200 {mobileOpen ? 'opacity-0' : ''}"></span>
            <span class="block w-5 h-0.5 bg-[var(--color-text)] transition-all duration-200 origin-center {mobileOpen ? '-rotate-45 -translate-y-[4px]' : ''}"></span>
        </button>
    </nav>

    <!-- Mobile menu -->
    {#if mobileOpen}
        <div class="md:hidden border-t border-[var(--color-border)] bg-[var(--color-bg)]">
            <ul class="px-6 py-4 flex flex-col gap-4">
                {#each navLinks as link}
                    <li>
                        <a
                            href={link.href}
                            class="text-base font-medium transition-colors duration-200
                                {page.url.pathname === link.href
                                    ? 'text-[var(--color-accent)]'
                                    : 'text-[var(--color-text-secondary)] hover:text-[var(--color-text)]'}"
                            onclick={closeMobile}
                        >
                            {link.label}
                        </a>
                    </li>
                {/each}
            </ul>
        </div>
    {/if}
</header>
