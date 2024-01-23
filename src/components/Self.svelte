<script>
    import Card from "./Card.svelte";
    export let self, liker
</script>

<div>
    {#if self != null}
        <Card card={self}/>
    {/if}

    {#if liker != null}
        <Card card={liker}/>
    {/if}
</div>

<style>
    div{
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        align-items: center;
        gap: 1.5 rem;
    }
</style>