<script>
    import SEO from '$lib/components/SEO.svelte';

    const selectedWork = [
        {
            title: 'E-Commerce Redesign',
            disciplines: ['Design', 'Development'],
            summary: 'A complete redesign of a fashion brand\'s online store, improving conversion rates by 40% through better UX and performance optimization.'
        },
        {
            title: 'SaaS Dashboard',
            disciplines: ['Development'],
            summary: 'Built a real-time analytics dashboard for a B2B startup, handling complex data visualization with clean, intuitive interfaces.'
        },
        {
            title: 'Brand Identity System',
            disciplines: ['Design'],
            summary: 'Developed a cohesive visual identity for an emerging wellness brand — logo, color system, typography, and brand guidelines.'
        }
    ];
</script>

<SEO
    title="Mai"
    description="Designer and developer crafting thoughtful digital experiences. Available for freelance projects."
/>

<!-- Hero -->
<section class="max-w-5xl mx-auto px-6 pt-24 pb-20 md:pt-32 md:pb-28">
    <p class="text-sm font-medium tracking-widest uppercase text-[var(--color-accent)] mb-4">
        Design &amp; Development
    </p>
    <h1 class="font-heading max-w-3xl">
        Crafting thoughtful digital experiences that connect.
    </h1>
    <p class="text-lg md:text-xl text-[var(--color-text-secondary)] max-w-2xl mt-6 leading-relaxed">
        I'm Mai — a multi-discipline freelancer helping brands and startups bring their ideas to life through design and code.
    </p>
    <div class="mt-10 flex flex-wrap gap-4">
        <a
            href="/about"
            class="inline-flex items-center gap-2 px-6 py-3 bg-[var(--color-accent)] text-white rounded-lg font-medium text-sm hover:bg-[var(--color-accent-hover)] transition-colors duration-200"
        >
            Learn more about me
        </a>
        <a
            href="mailto:hello@example.com"
            class="inline-flex items-center gap-2 px-6 py-3 border border-[var(--color-border)] text-[var(--color-text)] rounded-lg font-medium text-sm hover:border-[var(--color-accent)] hover:text-[var(--color-accent)] transition-colors duration-200"
        >
            Get in touch
        </a>
    </div>
</section>

<!-- Selected Work -->
<section class="max-w-5xl mx-auto px-6 py-16 border-t border-[var(--color-border)]">
    <p class="text-sm font-medium tracking-widest uppercase text-[var(--color-accent)] mb-2">
        Portfolio
    </p>
    <h2 class="font-heading mb-12">Selected work</h2>

    <div class="grid gap-8 md:grid-cols-3">
        {#each selectedWork as project}
            <article class="group p-6 rounded-xl border border-[var(--color-border)] bg-[var(--color-surface)] hover:border-[var(--color-accent)]/30 hover:shadow-lg hover:shadow-[var(--color-accent)]/5 transition-all duration-300">
                <div class="flex flex-wrap gap-2 mb-4">
                    {#each project.disciplines as tag}
                        <span class="text-xs font-medium tracking-wide uppercase px-2.5 py-1 rounded-full bg-[var(--color-accent)] text-white">
                            {tag}
                        </span>
                    {/each}
                </div>
                <h3 class="font-heading text-xl text-[var(--color-bg)] group-hover:text-[var(--color-accent)] transition-colors duration-200">
                    {project.title}
                </h3>
                <p class="text-sm text-[var(--color-text-secondary)] leading-relaxed mt-2">
                    {project.summary}
                </p>
            </article>
        {/each}
    </div>
</section>

<!-- CTA -->
<section class="max-w-5xl mx-auto px-6 py-20 border-t border-[var(--color-border)] text-center">
    <h2 class="font-heading mb-4">Let's work together</h2>
    <p class="text-[var(--color-text-secondary)] max-w-lg mx-auto mb-8 leading-relaxed">
        Have a project in mind? I'd love to hear about it. Whether it's a brand refresh, a new web app, or something in between — let's chat.
    </p>
    <a
        href="mailto:hello@example.com"
        class="inline-flex items-center gap-2 px-8 py-3.5 bg-[var(--color-accent)] text-white rounded-lg font-medium hover:bg-[var(--color-accent-hover)] transition-colors duration-200"
    >
        Say hello →
    </a>
</section>
