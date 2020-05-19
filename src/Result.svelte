<script>
import {createEventDispatcher} from 'svelte'
import {slide} from "svelte/transition"
export let data;
export let showResult;

const dispatch = createEventDispatcher();
</script>
{#if (showResult)}
<ul transition:slide={{y:100,duration:700}}>
    {#each data as value (value.id)}
    <li on:click={()=> dispatch('show',{value:value.id})} class="result">{value.title} - {value.artist.name}</li>
    {/each}
</ul>
{/if}

<style>
    ul{
    margin: 0px;
    padding: 0px;
    list-style-type: none;
    padding-top: 10px;
    margin-bottom: -20px;
    width: 100%;
    }

    li{
    border-bottom: 1px solid #5fdde5;
    padding-left: 20px;
    padding-right: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
    cursor: pointer;
    }

    li:last-child{
        border-bottom: none;
    }

    li:hover{
        background-color: rgba(255, 255, 255, 0.05);
    }
</style>