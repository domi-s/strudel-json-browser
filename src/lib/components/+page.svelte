<script>
    import Section from '$lib/components/Section.svelte';
    import SectionContent from '$lib/components/SectionContent.svelte';
	import StrudelJsonBrowserGraphic from '$lib/components/StrudelJsonBrowserGraphic.svelte';
	import VinylGraphic from '$lib/components/VinylGraphic.svelte';

    const borderStyle = "border-2 border-solid border-black";
</script>

<Section>
    <SectionContent class="flex flex-wrap gap-x-2 items-center text-sm font-medium">
        <VinylGraphic />
        <p>Strudel JSON Browser</p>
    </SectionContent>
</Section>
<Section>
    <SectionContent class="flex flex-col items-center justify-center">
        <StrudelJsonBrowserGraphic />
    </SectionContent>
</Section>
<Section>
    <SectionContent class={borderStyle + " p-2 text-xs relative -bottom-[.125rem]"}>
        Enter your JSON's URL &darr;
    </SectionContent>
    <input type="text" class={borderStyle + " w-full p-2"} placeholder="For instance, https://samples.grbt.com.au/strudel.json" />
</Section>
<Section>
    <SectionContent class={borderStyle + " p-4"}>
    </SectionContent>
</Section>