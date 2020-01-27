<script>
    import { fade } from 'svelte/transition'
    export let titles;
    export let swap;
</script>

<style>
    div {
        display: flex;
        flex-direction: column;
        position: absolute;
        top: 0;
        left: 0;
        height: 100%;
        width: 100%;
        z-index: 10;
        background-color: rgba(0, 0, 0, 0.3);
        justify-content: center;
        align-content: center;
        color: white;
    }
    div:hover {
        cursor: pointer;
    }
    h2{
        margin: 0;
    }
</style>


<div on:click={swap} transition:fade>
    <h1>{titles.main}</h1>
    {#if titles.sub}
    <h2>{titles.sub}</h2>
    {/if}
</div>