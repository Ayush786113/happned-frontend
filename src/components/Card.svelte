<script>
    import { onMount } from "svelte";

    export let card
    const gender = {
        "female": "F",
        "male": "M"
    }

    let picsmodal

    onMount(() => {
        picsmodal = document.getElementById('picsmodal')
    })

    function fullProfile(){
        picsmodal.addAttribute("open", "open")
    }
    function closemodal(){
        picsmodal.removeAttribute("open")
    }
</script>
{#if card != null}
<article>
    <header>
        <img src="{card.photos[0]}" alt="{card.ids[0]}">
    </header>
    <blockquote>
        <textarea readonly>{card.about}</textarea>
        <footer>
          <cite>- {card.name}</cite>
        </footer>
    </blockquote>
    <span>
        {gender[card.gender]}
        {card.age}
        {card.city === undefined ? "" : card.city}
        {#if card.verified}
            <i class="fa-solid fa-certificate"></i>
        {:else}
            <i class="fa-duotone fa-certificate"></i>
        {/if}
    </span>
    <footer>
        <div class="grid">
            <button class="contrast outline" disabled>Reject</button>
            <button disabled>Accept</button>
        </div>
    </footer>
</article>

<!-- <dialog id="picsmodal">
    <article>
      <div>
        {#each card.photos as photo}
        <img src="photo" alt="{card.name}">
        {/each}
      </div>
      <button on:click={closemodal}>Close</button>
    </article>
</dialog> -->
{/if}
<style>
    img{
        width: 250px;
        height: auto
    }
    /* div{
        display: flex;
        flex-wrap: wrap;
    } */
</style>