<script>
    const year = new Date().getFullYear();

    const socialLinks = [
        { label: 'GitHub', href: 'https://github.com' },
        { label: 'LinkedIn', href: 'https://linkedin.com' }
    ];
</script>

<footer class="mt-auto border-t border-[var(--color-border)]">
    <div class="max-w-5xl mx-auto px-6 py-12 flex flex-col sm:flex-row items-center justify-between gap-4">
        <p class="text-sm text-[var(--color-text-secondary)]">
            &copy; {year} Mai. All rights reserved.
        </p>
        <div class="flex items-center gap-6">
            {#each socialLinks as link}
                <a
                    href={link.href}
                    target="_blank"
                    rel="noreferrer"
                    class="text-sm text-[var(--color-text-secondary)] hover:text-[var(--color-accent)] transition-colors duration-200"
                >
                    {link.label}
                </a>
            {/each}
        </div>
    </div>
</footer>
