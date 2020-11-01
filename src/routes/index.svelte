<script>
import { onMount } from "svelte";
let players = [];
onMount(async () => {
	console.log("Getting players")
    await fetch(`http://premierleaguefantasy.site/players`,{
		mode: 'cors',
	})
	.then(response => response.json())
	.then(
		(data) => {
			players = data
			console.log(players[0])
		})
  })
</script>

<style>
	
</style>

<svelte:head>
	<title>Sapper project template</title>
</svelte:head>

<h1 class="font-bold">Players</h1>

	{#each players as player}
		<li>
			{player.first_name} {player.second_name} 
		</li>
	{/each}