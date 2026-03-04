<script>
    import vinyl1 from '$lib/assets/vinyl-1.svg';
    import vinyl2 from '$lib/assets/vinyl-2.svg';
</script>

<div class="w-6 h-6 relative">
    <img src={vinyl1} alt="Vinyl 1" class="vinyl-1 w-full h-full" />
    <img src={vinyl2} alt="Vinyl 2" class="vinyl-2 w-full h-full absolute top-0 left-0 opacity-0" />
</div>

<style>
    @keyframes alternate-vinyls-1 {
        0%, 50% { opacity: 1; }
        51%, 100% { opacity: 0; }
    }

    @keyframes alternate-vinyls-2 {
        0%, 50% { opacity: 0; }
        51%, 100% { opacity: 1; }
    }

    .vinyl-1 {
        animation: alternate-vinyls-1 750ms linear infinite;
    }

    .vinyl-2 {
        animation: alternate-vinyls-2 750ms linear infinite;
    }
</style>