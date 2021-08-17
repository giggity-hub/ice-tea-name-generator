<script>
    import fitty from 'fitty';
    import { onMount } from 'svelte';
    let ref;

    export let minSize = 10;
    export let maxSize = 100;
    export let text;

    onMount(async ()=>{
        fitty(ref, {
            minSize,
            maxSize
        });
    })

</script>

<span bind:this={ref}>{text}</span>


