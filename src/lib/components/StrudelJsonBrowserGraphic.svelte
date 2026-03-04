<script>
    import strudelJsonBrowser1 from '$lib/assets/strudel-json-browser-1.svg';
    import strudelJsonBrowser2 from '$lib/assets/strudel-json-browser-2.svg';
    import strudelJsonBrowser3 from '$lib/assets/strudel-json-browser-3.svg';
</script>

<div class="w-48 h-16 relative">
    <img src={strudelJsonBrowser1} alt="Strudel JSON Browser 1" class="strudel-json-browser-1 w-full h-full" />
    <img src={strudelJsonBrowser2} alt="Strudel JSON Browser 2" class="strudel-json-browser-2 w-full h-full absolute top-0 left-0 opacity-0" />
    <img src={strudelJsonBrowser3} alt="Strudel JSON Browser 3" class="strudel-json-browser-3 w-full h-full absolute top-0 left-0 opacity-0" />
</div>

<style>
    @keyframes alternate-text-1 {
        0%, 33% { opacity: 1; }
        34%, 66% { opacity: .15; }
        67%, 100% { opacity: 0; }
    }

    @keyframes alternate-text-2 {
        0%, 33% { opacity: 0; }
        34%, 66% { opacity: 1; }
        67%, 100% { opacity: .15; }
    }

    @keyframes alternate-text-3 {
        0%, 33% { opacity: .15; }
        34%, 66% { opacity: 0; }
        67%, 100% { opacity: 1; }
    }

    .strudel-json-browser-1 {
        animation: alternate-text-1 750ms linear infinite;
    }

    .strudel-json-browser-2 {
        animation: alternate-text-2 750ms linear infinite;
    }

    .strudel-json-browser-3 {
        animation: alternate-text-3 750ms linear infinite;
    }
</style>