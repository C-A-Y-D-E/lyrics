<script>
    export let lyrics;
    export let copy;
    export let lyricsTitle;
   
</script>
{#if (lyrics.error)}
<div class="error">
    {lyrics.error}
</div>

{:else}
<div class="lyrics">
    <h3 class="lyrics-title">{lyricsTitle}</h3>
    <div on:click class="copy-lyrics">
        {copy}
    </div>
    <div class="thelyrics">{@html lyrics.lyrics.replace(/(\r\n|\r|\n)/g,'<br>')}</div>
</div>
{/if}

<style>
    h3{
        text-align: center;
    }

    .copy-lyrics{
    text-align: right;
    cursor: pointer;
    color: #5fdde5;
    text-transform: uppercase;
    font-family: 'Open Sans', sans-serif;

    }

    .thelyrics{
        display: flex;
        justify-content: center;
        
    }

    .error{
        text-align: center;
        font-size: 2rem;
    }
</style>