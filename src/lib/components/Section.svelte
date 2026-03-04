<script>
    let props = $props();
</script>

<div class={["max-w-screen-xl mx-auto p-4", props.class]}>
    <slot />
</div>