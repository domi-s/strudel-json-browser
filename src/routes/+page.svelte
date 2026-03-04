<script lang="ts">
	import EnterYourJsonUrlGraphic from '$lib/components/EnterYourJsonUrlGraphic.svelte';
	import SamplesFoundGraphic from '$lib/components/SamplesFoundGraphic.svelte';
    import Section from '$lib/components/Section.svelte';
    import SectionContent from '$lib/components/SectionContent.svelte';
	import StrudelJsonBrowserGraphic from '$lib/components/StrudelJsonBrowserGraphic.svelte';
	import VinylGraphic from '$lib/components/VinylGraphic.svelte';
	import { error } from '@sveltejs/kit';

    import { slide } from 'svelte/transition';

    const borderStyle = "border-2 border-solid border-black";

    const defaultJsonUrl = "https://samples.grbt.com.au/strudel.json";

    let results: unknown = null;
    let loading = false;
    let errorInformation: string | null = null;
    let jsonUrl = "";
    let audio: HTMLAudioElement | null = null;
    let audioCurrentTime = 0;
    let audioDuration = 0;

    async function loadJson() {
        if(loading) return;

        let url = jsonUrl.trim();
        if (url === "")
            url = defaultJsonUrl;

        loading = true;
        results = null;
        errorInformation = null;

        try {
            const response = await fetch(url);

            if(!response.ok) {
                throw new Error(`HTTP error! Status: ${response.status}`);
            }

            results = await response.json();
            loading = false;
        } catch(err) {
            loading = false;
            errorInformation = err instanceof Error ? err.message : String(err);
        }
    }

    function playAudio(postUrl: string) {
        if(!results) {
            errorInformation = "No JSON loaded. Please load a JSON file first.";
            return;
        }

        if(typeof results !== 'object' || results === null) {
            errorInformation = "The loaded JSON must be an object.";
            return;
        }

        if(!('_base' in results) || typeof results['_base'] !== 'string') {
            errorInformation = "The JSON must contain a '_base' property with the base URL for the audio files.";
            return;
        }

        const url = results['_base'] + postUrl.trim();

        audio = new Audio(url);
        audio.addEventListener('timeupdate', () => {
            audioCurrentTime = audio!.currentTime;
        });
        audio.addEventListener('loadedmetadata', () => {
            audioDuration = audio!.duration;
        });
        audio.play();
        console.log(audio);
    }

    function stopAudio() {
        if(audio) {
            audio.pause();
            audio.currentTime = 0;
            audio = null;
            audioCurrentTime = 0;
            audioDuration = 0;
        }
    }
</script>

<Section>
    <SectionContent class="flex flex-wrap gap-x-4 items-center justify-center text-sm font-medium">
        <VinylGraphic />
        <StrudelJsonBrowserGraphic />
    </SectionContent>
    <SectionContent class="text-center">
        <p class="text-xs opacity-50 font-medium">App & Design by <a href="https://github.com/domi-s" target="_blank" class="underline decoration-dashed">Dominic Satnoianu</a></p>
    </SectionContent>
</Section>
<Section>
    <SectionContent class="flex flex-col items-center justify-center">
        <EnterYourJsonUrlGraphic />
    </SectionContent>
    <SectionContent class="flex flex-col items-center justify-center relative -top-12 w-full">
        <input type="text" class={borderStyle + " w-full max-w-sm p-2"} style="border-style: dashed;" placeholder="Type here&hellip;" bind:value={jsonUrl} on:keydown={e => e.key === 'Enter' && loadJson()} />
        <div class="relative">
            {#if jsonUrl.trim() == ""}
                <p class="w-full text-center text-xs mt-2" transition:slide={{ duration: 200 }}>For instance, https://samples.grbt.com.au/strudel.json</p>
            {:else}
                <p class="w-full text-center text-xs mt-2" transition:slide={{ duration: 200 }}>Press Enter to load the JSON from the URL above.</p>
            {/if}
        </div>
    </SectionContent>
</Section>
{#if errorInformation}
    <Section>
        <SectionContent class="flex flex-col items-center justify-center">
            <p class="text-sm text-red-500 font-medium">{errorInformation}</p>
        </SectionContent>
    </Section>
{:else if loading}
    <Section>
        <SectionContent class="flex flex-col gap-y-4 items-center justify-center">
            <div class="scale-200">
                <VinylGraphic />
            </div>
            <p class="text-sm">Loading&hellip;</p>
        </SectionContent>
    </Section>
{:else if results}
    <Section>
        <SectionContent class="flex flex-wrap gap-x-4 items-center justify-center text-sm font-medium">
            <VinylGraphic />
            <SamplesFoundGraphic />
            <VinylGraphic />
        </SectionContent>
    </Section>
    <Section>
        <SectionContent class="flex flex-col gap-y-4 items-start justify-center w-full">
            {#each Object.entries(results) as [key, value]}
                {#if Array.isArray(value)}
                    <div class="w-full">
                        <h3 class="font-black sticky top-0 bg-white py-4 z-50">Category: {key}</h3>
                        <div class="flex flex-col gap-y-2 mt-1 mb-4 w-full">
                            {#each value as item, index}
                                <div class="border-2 border-solid border-black p-2 w-full flex flex-col leading-tight">
                                    <span class="text-xs opacity-75">{key}:{index}</span>
                                    <p>{item}</p>
                                    <div class="mt-2 flex flex-wrap gap-x-2 gap-y-1 items-center">
                                        {#if audio && audio.src.endsWith(item.trim())}
                                            <button class="text-xs font-bold hover:underline decoration-dashed cursor-pointer" on:click={stopAudio}>Stop</button>
                                            <p class="text-xs opacity-50">
                                                {#if audioCurrentTime}
                                                    {audioCurrentTime.toFixed(1)}s / {audioDuration ? audioDuration.toFixed(1) : '??'}s
                                                {:else}
                                                    Loading&hellip;
                                                {/if}
                                            </p>
                                        {:else}
                                            <button class="text-xs font-bold hover:underline decoration-dashed cursor-pointer" on:click={() => playAudio(item)}>Play</button>
                                        {/if}
                                    </div>
                                </div>
                            {/each}
                        </div>
                    </div>
                {/if}
            {/each}

        </SectionContent>
    </Section>
{/if}