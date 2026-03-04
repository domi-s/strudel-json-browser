<script>
	import EnterYourJsonUrlGraphic from '$lib/components/EnterYourJsonUrlGraphic.svelte';
	import SamplesFoundGraphic from '$lib/components/SamplesFoundGraphic.svelte';
    import Section from '$lib/components/Section.svelte';
    import SectionContent from '$lib/components/SectionContent.svelte';
	import StrudelJsonBrowserGraphic from '$lib/components/StrudelJsonBrowserGraphic.svelte';
	import VinylGraphic from '$lib/components/VinylGraphic.svelte';

    import { slide } from 'svelte/transition';

    const borderStyle = "border-2 border-solid border-black";

    let results = null;
    let jsonUrl = "";
</script>

<Section>
    <SectionContent class="flex flex-wrap gap-x-4 items-center justify-center text-sm font-medium">
        <VinylGraphic />
        <StrudelJsonBrowserGraphic />
    </SectionContent>
</Section>
<Section>
    <SectionContent class="flex flex-col items-center justify-center">
        <EnterYourJsonUrlGraphic />
    </SectionContent>
    <SectionContent class="flex flex-col items-center justify-center relative -top-12 w-full">
        <input type="text" class={borderStyle + " w-full max-w-sm p-2"} placeholder="Type here&hellip;" bind:value={jsonUrl} />
        <div class="relative">
            <p class="opacity-0 pointer-events-none select-none">For instance, https://samples.grbt.com.au/strudel.json</p>
            {#if jsonUrl.trim() == ""}
                <p class="absolute top-0 w-full text-center text-xs mt-2" transition:slide={{ duration: 200 }}>For instance, https://samples.grbt.com.au/strudel.json</p>
            {:else}
                <p class="absolute top-0 w-full text-center text-xs mt-2" transition:slide={{ duration: 200 }}>Press Enter to load the JSON from the URL above.</p>
            {/if}
        </div>
    </SectionContent>
</Section>
{#if results}
    <Section>
        <SectionContent class="flex flex-wrap gap-x-4 items-center justify-center text-sm font-medium">
            <VinylGraphic />
            <SamplesFoundGraphic />
            <VinylGraphic />
        </SectionContent>
    </Section>
{/if}