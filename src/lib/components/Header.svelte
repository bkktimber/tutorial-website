<script>
    export let siteTitle = "My Personal Site";
</script>

<header class="glass-panel">
    <div class="container">
        <a href="/" class="brand">{siteTitle}</a>
        <nav>
            <a href="/">Home</a>
            <a href="/about">About</a>
            <a href="/projects">Projects</a>
            <a href="/contact">Contact</a>
        </nav>
    </div>
</header>

<style>
    header {
        position: fixed;
        top: var(--spacing-md);
        left: 50%;
        transform: translateX(-50%);
        width: calc(100% - var(--spacing-lg));
        max-width: 1200px;
        z-index: 100;
        padding: var(--spacing-md) var(--spacing-lg);
    }

    .container {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .brand {
        font-family: var(--font-heading);
        font-weight: 700;
        font-size: 1.25rem;
        color: var(--color-text-primary);
        text-transform: uppercase;
        letter-spacing: 1px;
    }

    nav {
        display: flex;
        gap: var(--spacing-lg);
    }

    nav a {
        font-size: 0.95rem;
        color: var(--color-text-secondary);
        font-weight: 500;
    }

    nav a:hover {
        color: var(--color-accent);
    }

    /* Mobile Responsive adjustments could go here with media queries */
    @media (max-width: 768px) {
        nav {
            gap: var(--spacing-md);
        }
        header {
            width: calc(100% - var(--spacing-md));
            padding: var(--spacing-sm) var(--spacing-md);
        }
    }
</style>
