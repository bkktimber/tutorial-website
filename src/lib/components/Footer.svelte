<script>
    const year = new Date().getFullYear();
</script>

<footer>
    <div class="container">
        <p>&copy; {year} My Personal Site. All rights reserved.</p>
        <div class="socials">
            <a href="https://github.com" target="_blank" rel="noreferrer">GitHub</a>
            <a href="https://linkedin.com" target="_blank" rel="noreferrer">LinkedIn</a>
            <a href="https://twitter.com" target="_blank" rel="noreferrer">Twitter</a>
        </div>
    </div>
</footer>

<style>
    footer {
        margin-top: var(--spacing-xl);
        padding: var(--spacing-xl) 0;
        border-top: 1px solid rgba(255, 255, 255, 0.05);
    }

    .container {
        display: flex;
        justify-content: space-between;
        align-items: center;
        max-width: 1280px;
        margin: 0 auto;
        padding: 0 var(--spacing-md);
    }

    p {
        color: var(--color-text-secondary);
        font-size: 0.9rem;
    }

    .socials {
        display: flex;
        gap: var(--spacing-md);
    }
    
    .socials a {
        color: var(--color-text-secondary);
        font-size: 0.9rem;
    }

    .socials a:hover {
        color: var(--color-text-primary);
    }
</style>
