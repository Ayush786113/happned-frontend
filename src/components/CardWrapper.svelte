<script>
    import Card from "./Card.svelte";

    export let cards
</script>

<div class="container">
    {#if cards != null}
        {#each cards as card}
            <Card card={card}/>
        {/each}
    {/if}
</div>

<style>
    div{
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        align-items: center;
        gap: 1.5rem;
    }
</style>