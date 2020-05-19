<script>
    export let search;
    export let getSongData;
</script>
<div class="search">
    <form on:submit|preventDefault={getSongData}>
        <input type="search" bind:value="{search}" placeholder="Type Song Name For Lyrics">
    </form>
    
    <slot></slot>
</div>

<style>
    .search{
    margin: 20px;
    padding: 20px;
    }

    input:focus{
        outline: none;
    }
    input{
    width: 100%;
    background: none;
    border-top: none;
    border-left: none;
    border-bottom: 1px solid #5fdde5;
    color: white;
    height: 30px;
    border-right: none;
    font-size: 16px;
    }
</style>