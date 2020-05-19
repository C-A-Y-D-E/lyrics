<script>
	import Search from "./Search.svelte"
	import Result from "./Result.svelte"
	import Lyrics from "./Lyrics.svelte"
	import Container from "./Container.svelte"
	 let search = '';
	 let showLyrics = false;
	 let data = [];
	 let lyricsFilter = [];
	 let lyrics = '';
	 let showResult = false;
	 let copy = 'Copy lyrics';
	 let lyricsTitle = '';

	const getSongData  = async()=>{
		if(search.trim()){
		const res = await fetch(`https://api.lyrics.ovh/suggest/${search}`) 
		let value = await res.json()
		data = value.data
		showResult = true;
		}else{
			data = []
			showLyrics = false;
		}
		
	}

	function lyricsShow(event){
		let clickLyrics = event.detail.value
		lyricsFilter = data.filter(ly=> ly.id === clickLyrics)
		getLyrics(lyricsFilter);
		lyricsTitle = lyricsFilter[0].title
	}

const getLyrics = async (lyricsFilter)=>{
	
	const res = await fetch(`https://api.lyrics.ovh/v1/${lyricsFilter[0].artist.name}/${lyricsFilter[0].title}`)
	const data = await res.json()
	lyrics = data;
	showResult = false;
	showLyrics = true;

}

function copyText(event){
 window.navigator.clipboard.writeText(event.target.nextElementSibling.innerText)
 copy = 'Copied To ClipBoard'
}


</script>
<svelte:head>
	<link href="https://fonts.googleapis.com/css2?family=Bungee+Shade&display=swap" rel="stylesheet">
</svelte:head>
<Container>
	<div class="title">
		Lyrics Search Web App
	</div>
	<Search bind:search {getSongData}>
		{#if (Object.keys(data).length > 0)}
		<Result {data} on:show={lyricsShow} {showResult} />
		{/if}
	</Search>
	{#if (showLyrics)}
	<Lyrics {copy} {lyricsTitle} on:click={copyText} {lyrics}/>
	{/if}
	
</Container>


<style>
	:global(body){
	background-color: #333;
    color: white;
    margin: 0px;
    padding: 0px;
    min-height: 100%;
    position: relative;
	}

	.title{
		width: 100%;
		font-size: 3rem;
		text-align: center;
		margin-top: 20px;
		font-family: 'Bungee Shade', cursive;
		color: #5fdde5;
}
	
</style>