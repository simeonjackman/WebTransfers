<script context="module">
	export async function preload() {
		const res = await this.fetch(`http://premierleaguefantasy.site/players?sort_by=transfers_in_event`);
		const data = await res.json();

		if (res.status === 200) {
			return { players: data };
		} else {
			this.error(res.status, data.message);
		}
	}
</script>

<script>
	export let players;
</script>

<style>
	ul {
		margin: 0 0 1em 0;
		line-height: 1.5;
	}
</style>

<svelte:head>
	<title>Players</title>
</svelte:head>

<h1 class="px-6 py-3 bg-gray-900 text-left text-xl leading-4 font-medium text-gray-500 uppercase tracking-wider">Players</h1>
<ul>
	{#each players as player}
		<li class="cursor-pointer hover:bg-gray-500 hover:text-gray-900 px-6 py-3 bg-gray-50 text-left text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider"><a rel="prefetch" href="players/{player.id}">{player.first_name} {player.second_name}</a></li>
	{/each}
</ul>
