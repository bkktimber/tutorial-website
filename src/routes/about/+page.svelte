<script>
    import SEO from '$lib/components/SEO.svelte';

    const skills = [
        { category: 'Design', items: ['UI/UX Design', 'Brand Identity', 'Design Systems', 'Prototyping'] },
        { category: 'Development', items: ['SvelteKit', 'React / Next.js', 'TypeScript', 'CSS / Tailwind'] },
        { category: 'Tools', items: ['Figma', 'Git', 'Sanity CMS', 'Vercel'] }
    ];
</script>

<SEO
    title="About"
    description="Learn more about Mai — a multi-discipline designer and developer crafting digital experiences for brands and startups."
/>

<section class="max-w-5xl mx-auto px-6 pt-24 pb-16 md:pt-32">
    <p class="text-sm font-medium tracking-widest uppercase text-[var(--color-accent)] mb-4">
        About
    </p>
    <h1 class="font-heading max-w-3xl">
        A bit about me.
    </h1>
</section>

<!-- Story -->
<section class="max-w-5xl mx-auto px-6 pb-16">
    <div class="max-w-2xl space-y-6 text-[var(--color-text-secondary)] leading-relaxed">
        <p class="text-lg">
            I'm a designer and developer who loves the intersection of aesthetics and engineering. I believe the best digital products are the ones that feel effortless to use — and that takes a lot of careful effort to build.
        </p>
        <p>
            Over the years, I've worked with startups, agencies, and independent brands to bring ideas from concept to launch. My background spans product design, frontend development, and brand strategy — which means I can take a project from wireframe to deployed code.
        </p>
        <p>
            When I'm not at my desk, you'll probably find me exploring new coffee shops, reading about typography, or tinkering with side projects that may or may not ever see the light of day.
        </p>
    </div>
</section>

<!-- What I Do -->
<section class="max-w-5xl mx-auto px-6 py-16 border-t border-[var(--color-border)]">
    <p class="text-sm font-medium tracking-widest uppercase text-[var(--color-accent)] mb-2">
        Capabilities
    </p>
    <h2 class="font-heading mb-12">What I work with</h2>

    <div class="grid gap-8 md:grid-cols-3">
        {#each skills as group}
            <div class="p-6 rounded-xl border border-[var(--color-border)] bg-[var(--color-surface)]">
                <h3 class="font-heading text-lg mb-4 text-[var(--color-accent)]">{group.category}</h3>
                <ul class="space-y-2">
                    {#each group.items as item}
                        <li class="text-sm text-[var(--color-text-secondary)]">{item}</li>
                    {/each}
                </ul>
            </div>
        {/each}
    </div>
</section>

<!-- CTA -->
<section class="max-w-5xl mx-auto px-6 py-20 border-t border-[var(--color-border)] text-center">
    <h2 class="font-heading mb-4">Want to work together?</h2>
    <p class="text-[var(--color-text-secondary)] max-w-lg mx-auto mb-8 leading-relaxed">
        I'm always open to interesting projects and collaborations. Drop me a line and let's see what we can create.
    </p>
    <a
        href="mailto:hello@example.com"
        class="inline-flex items-center gap-2 px-8 py-3.5 bg-[var(--color-accent)] text-white rounded-lg font-medium hover:bg-[var(--color-accent-hover)] transition-colors duration-200"
    >
        Get in touch →
    </a>
</section>
